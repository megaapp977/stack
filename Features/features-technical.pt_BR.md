# MEGA - Detalhe Tecnico de Funcionalidades (PT-BR)

Versao: Enterprise
Ultima atualizacao: 15 de julho de 2026
Idioma: Portugues (Brasil)

## 1. Objetivo

Este documento descreve como as funcionalidades principais da MEGA estao implementadas do ponto de vista tecnico.
Ele complementa [features.pt_BR.md](features.pt_BR.md), que e voltado para apresentacao comercial.

## 2. Stack base e arquitetura

- Backend principal: Ruby on Rails.
- Frontend dashboard: Vue 3.
- Overlay Enterprise: extensoes e overrides em enterprise.
- Processamento assincrono: Sidekiq para jobs em background.
- Camada realtime: Action Cable para conversas, salas e quadros.
- Persistencia: PostgreSQL como banco principal.
- Seguranca de API: politicas de permissao e controle por papel.

## 3. Dominios funcionais

### 3.1 Canais de mensagens e voz

- WhatsApp Cloud API: canal oficial com templates e eventos de entrega.
- Mega Hub para Meta: modo opcional no Super Admin para conectar WhatsApp, Messenger e Instagram usando apps compartilhados do Hub; o bloco de credenciais do Hub é configurado em Super Admin → Mega Hub, e as caixas criadas continuam enviando pelos serviços nativos e recebem eventos reenviados por webhook.
- Saúde da conexão do WhatsApp Cloud: falhas de token manual são exibidas sem bloquear o processamento de webhooks recebidos, enquanto o cadastro integrado mantém o fluxo de reautorização.
- WhatsApp Evolution, WAHA e Uazapi: provedores alternativos com suporte multimidia e grupos.
- Estado de conexão por provedor: WAHA, Evolution e Uazapi usam suas próprias APIs e webhooks; a validação de assinatura da Meta fica reservada ao WhatsApp Cloud.
- Vinculação WAHA com passkey: detecção proativa da extensão via `WAHA_PASSKEY_CHROME_EXTENSION_ID`, estados `PASSKEY_REQUIRED` e `PASSKEY_CONFIRMATION_REQUIRED` dentro de `session.status`, challenge por `/auth/passkey/challenge`, fluxo temporário por token para asserção, assinatura com extensão de navegador em `web.whatsapp.com` e confirmação manual por código; os GET sem dados pendentes retornam `422`.
- Sincronização global sob demanda para WAHA e Uazapi: jobs Sidekiq com progresso em Redis, janelas de 24h/7d, deduplicação por ids do provedor, reutilização de conversas abertas, download assíncrono de mídia histórica, bloqueio de concorrência por conta e worker dedicado opcional `whatsapp_history_sync` para instalações de alto volume.
- Sincronização por conversa para WAHA e Uazapi: ação manual pelo menu da conversa, com janelas de 24h/7d e deduplicação por ids do provedor.
- Reações do WhatsApp: atores do dashboard e tokens de API podem adicionar, substituir e remover uma reação por mensagem preservando ecos do WhatsApp Device.
- Notificame: variante oficial orientada a operacao LATAM.
- Instagram, Facebook, TikTok, Telegram, X, SMS e Email como inboxes.
- Processamento de email IMAP com timeout dedicado para evitar jobs travados nas caixas de entrada.
- Inferencia do provedor de email a partir dos registros MX do dominio de cadastro para sugerir integracoes Gmail ou Outlook durante o onboarding.
- Upload de anexos com reconhecimento explicito de arquivos `.pfx` junto aos formatos comuns de midia e documentos.
- API Channel: gateway generico para plataformas proprietarias via API/webhooks.
- Voz Twilio e chamadas WhatsApp Cloud: fluxo WebRTC com timeline unificada; os relatorios Twilio normalizam dados a partir do modelo Call, as gravacoes nativas opcionais exigem aceite do custo de storage e as gravacoes aparecem nas conversas e no relatorio de chamadas.
- Controle de transcricao de audio: GPT-4o Mini Transcribe por padrao para notas de voz com Whisper disponivel como override por conta; as gravacoes mantem flags por conta para habilitacao geral e comportamento por provedor (WhatsApp Cloud e WaVoIP), normalizacao de audio, diarizacao por turno, transcricao fiel com GPT-4o Transcribe, rotulos baseados no nome do contato/agente atribuido e reprocessamento manual pelo menu contextual de mensagens de audio sem texto.
- WaVoIP com persistencia de sessao por inbox e reaproveitamento de credenciais conforme o papel do usuario.

### 3.2 Nucleo de conversas

- Modelo de status: open, pending, resolved, snoozed.
- Modelo de prioridade: tratamento de urgencia por conversa.
- Participantes: colaboracao multiagente na mesma thread.
- Rascunhos e fixadas: continuidade de trabalho por agente.
- Filtros avancados e visoes personalizadas: segmentacao para alto volume.
- Ordenacao dedicada por unread na lista de conversas.
- Filtros dedicados no sidebar: unread, mentions, participating, groups e unattended na navegacao de conversas.
- Contadores reativos no sidebar: unread por tipo de conversa e mentions via notification_type=conversation_mention.
- Assignment V2: distribuicao inteligente com capacidade e regras.
- Os inboxes expoem `auto_assign_on_agent_reply` para manter conversas nao atribuidas sem responsavel quando um agente envia uma mensagem de saida.
- Equipes: `icon` e `icon_color` sao persistidos em `teams`, expostos pela API/model JSON e incluidos nos payloads realtime para listas e seletores de atribuicao.
- SLA Enterprise: `AppliedSla` expoe prazos FRT/NRT/RT calculados no backend; quando a politica usa horario comercial, `Sla::BusinessHoursService` consome a configuracao de working hours do inbox e a resposta JSON entrega `sla_*_due_at` ao dashboard. Conversas com contato bloqueado rejeitam nova atribuicao de SLA, sao excluidas de processamento/relatorios e limpam `sla_policy_id`, `applied_sla` e `sla_events` dos payloads enquanto seguirem bloqueadas.
- Drilldown de relatorios V2: `/api/v2/accounts/:account_id/reports/drilldown` retorna as conversas, mensagens ou eventos que compoem uma barra do grafico; `V2::Reports::DrilldownBuilder` valida metrica, bucket, permissao de administrador, paginacao, filtros por conta/inbox/agente/equipe/etiqueta, horario comercial e serializacao da ultima mensagem, com rate limit dedicado no Rack::Attack.
- Respostas prontas com anexos reutilizaveis tambem nos fluxos de nova conversa.
- Editor de resposta com upload de imagens inline em Email e Widget Web, redimensionamento por ProseMirror e renderizacao segura de `cw_image_width`/`cw_image_height`.
- A resolucao de `reply_to` no WhatsApp respeita `conversation_history` buscando identificadores citados em conversas anteriores do mesmo contact inbox, sem ampliar a busca para todas as mensagens da conta.
- Fluxo de desligamento de agentes com revisao previa das conversas atribuidas e opcao de desatribuir ou reatribuir em lote respeitando acesso por inbox/equipe.

### 3.3 Comunicacao interna e salas

- Chat Rooms permanece como dominio proprio sobre a base existente: `chat_rooms`, `chat_room_members` e `chat_room_messages`.
- Paridade interna estendida com `chat_room_categories`, `chat_room_drafts`, `chat_room_reactions`, `chat_room_polls`, `chat_room_poll_options`, `chat_room_poll_votes` e `chat_room_teams`.
- Tipos de sala: `public_channel`, `private_channel` e `direct_message`, com nomes opcionais para DMs e reutilizacao de DMs existentes por combinacao de membros.
- API account-scoped para salas, membros, categorias, rascunhos, reacoes, enquetes, busca, leitura/unread, arquivo e status de digitacao.
- Busca com `f_unaccent` em canais, DMs e mensagens acessiveis por usuario.
- Vuex `chatRooms` centraliza salas, mensagens, replies de thread, categorias, rascunhos e resultados de busca; a UI expoe filtros, secoes, criacao rapida, DMs, rascunhos, enquetes, painel lateral de thread e edicao de canais pelo menu de acoes do cabecalho.
- Realtime via Action Cable e eventos `CHAT_ROOM_*` para criacao/atualizacao/exclusao de mensagens, salas, reacoes, enquetes, leitura e typing.
- Chamadas de audio/video WebRTC persistem o ciclo de vida em `chat_room_calls`, registram participantes em `chat_room_call_participants`, retransmitem SDP/ICE efemero pelo `RoomChannel` e reutilizam os tons `ring.mp3`/`calling.mp3`.
- Contas com `chat_room_calls` recebem apenas o `DEFAULT_STUN_URL` do Google; ao habilitar `premium_call_connectivity`, `Mega::Calls::IceConfig` carrega `MEGA_CALL_STUN_URLS`, `MEGA_CALL_TURN_URLS`, `MEGA_CALL_TURN_USERNAME` e `MEGA_CALL_TURN_CREDENTIAL` por meio de `GlobalConfigService`. Valores salvos em Super Admin > Call ICE têm prioridade, variáveis de ambiente existentes são migradas e TURN só é publicado quando os três campos TURN estão completos.
- O vídeo nativo normaliza câmera e tela como streams independentes, renegocia um sender de tela adicional sem interromper a câmera e renderiza um espaço limitado ou flutuante com palco de apresentação e trilho de participantes; o Rails autoriza o mute do grupo com base no iniciador e a topologia P2P continua destinada a pequenos grupos controlados.
- Chamadas ao vivo exigem ambas as features da conta, `chat_rooms` e `chat_room_calls`, esta última desabilitada por padrão; `premium_call_connectivity` apenas seleciona o transporte ICE. A API responde `403 feature_disabled` e o `RoomChannel` não retransmite SDP/ICE se alguma das duas features obrigatórias estiver desativada, enquanto as mensagens históricas permanecem visíveis.
- Chamadas com tres ou mais membros registram cada convidado como `pending`/`joined`/`declined`; o toque continua ate todos recusarem ou o iniciador encerrar a chamada.
- A audiencia vem de `OnlineStatusTracker`: uma chamada 1:1 nao e criada quando o destinatario esta offline, e grupos convidam apenas membros com presenca `online`.
- Cada chamada cria uma unica `chat_room_message` do tipo `voice_call`; o mesmo registro muda entre `ringing`, `in-progress`, `no-answer` e `completed`, alimentando o historico e a previa da sala em tempo real.
- O fluxo de áudio reutiliza o padrão visual do `FloatingCallWidget`: posicionamento lógico RTL/LTR, largura responsiva, tokens `n-call-widget-*`, hierarquia de status e identidade e controles circulares; preserva seu próprio estado WebRTC e mantém o vídeo isolado.
- Webhooks podem emitir eventos de chat rooms sem misturar o contrato de conversas com clientes.

### 3.4 Automacao e bots

Eventos suportados:

- Conversa criada e atualizada.
- Mensagem recebida e criada.

Condicoes:

- Status, inbox, etiquetas, idioma, atributos e conteudo.
- Nota privada como condicao para fluxos internos.

Acoes:

- Atribuir agente ou equipe.
- Atribuir ao ultimo agente que respondeu.
- Remover atribuicao de agente ou equipe.
- Etiquetar, alterar status/prioridade, enviar webhook, silenciar.

Bots:

- Agent Bots por inbox com handover inteligente; os seletores de atribuição manual exibem apenas bots ativos configurados em todos os inboxes solicitados.
- Typebot estendido com comandos MEGA_CMD para atribuicao de agente/equipe.
- Typebot ignora reacoes de WhatsApp para evitar inicios ou mensagens artificiais.
- Assinaturas de webhook por canal para validar autenticidade de eventos de saida.

### 3.5 IA Captain

- Provedores suportados: OpenAI, Anthropic, Google, Azure OpenAI, Bedrock, DeepSeek.
- Assistants: configuracao por inbox com instrucoes e contexto.
- Visao geral do assistente: endpoints Enterprise de estatisticas, drilldown e resumo cacheado baseados em `Captain::AssistantStatsBuilder`, `Captain::AssistantStatsWindow`, `Captain::AssistantDrilldownBuilder` e `Captain::OverviewSummaryService`; o tempo economizado estimado e derivado das respostas publicas do assistente usando uma suposicao fixa de 2 minutos de esforco do agente por resposta.
- Roteamento de modelos Captain por feature (`assistant`, `copilot`, `document_faq_generation`, `pdf_faq_generation`, `audio_transcription`, etc.) com override por conta e fallback para configuracao global.
- Captain Documents: upload, indexacao e auto-sincronizacao por plano com jitter, fila purgable, limites configuraveis por conta e globais e uma vista de detalhes com conteudo rastreado, metadados da fonte e quantidade de FAQs geradas.
- Captain Scenarios: regras de ativacao e prioridade.
- Captain Custom Tools: integracoes HTTP com GET, POST, PUT, PATCH e DELETE.
- MCP nativo por conta: endpoints dedicados por slug em /mcp/:account_id/:slug.
- OAuth MCP: metadata .well-known, register, authorize, token, refresh token e PKCE.
- Autenticacao dupla: Bearer OAuth ou Api-Access-Token estatico.
- Catalogo MCP curado para uso cotidiano: ferramentas com nomes estaveis por dominio (conversations, contacts, inboxes, help center, reports, kanban e outros).
- Tools MCP publicadas: base (account_context, account_actions_list, account_action_call) + catalogo curado; inclui leitura/busca de Help Center com `help_center_articles_list`, `help_center_articles_search`, `help_center_articles_get` e `help_center_categories_list`; dinamicas explicitas via allowed_tools.
- Auto-resolve mode: evaluated, legacy ou disabled por conta. O modo avaliado envia ao avaliador o status da conversa e o conteúdo rotulado das mensagens não privadas; transferências e acompanhamentos pendentes permanecem abertas.

### 3.6 CRM e gestao de contatos

- Atributos personalizados por tipo de dado e uso em automacoes.
- Visibilidade por papel para atributos sensiveis (Enterprise).
- Etiquetas em contatos e conversas.
- Empresas agrupadas por dominio com timeline unificada.
- Os payloads de contato expõem `company_id` quando Companies esta habilitado; atualizacoes de contato podem atribuir ou limpar a empresa e mantem `additional_attributes.company_name` sincronizado.
- Importacao e exportacao de contatos disponiveis para administradores e papeis Enterprise com permissao `contact_manage`.
- A importação do Intercom é exclusiva para administradores e protegida pela feature `data_import`; credenciais e mapeamentos persistentes são armazenados por conta.
- Páginas de contatos e conversas são processadas por jobs Sidekiq, com registros idempotentes de itens/mapeamentos, logs de ignorados/erros, execuções retomáveis e caixas de entrada API por origem.
- Bloqueio ativo no WhatsApp para descartar mensagens recebidas de contatos bloqueados.

### 3.7 Campanhas

- Ongoing campaigns para widget/live chat.
- One-off campaigns para WhatsApp, SMS e API Channel.
- Construtor de templates Meta com ciclo de aprovacao e sincronizacao.
- Controle de velocidade, rotacao multi-inbox e metricas de execucao.

### 3.8 Help Center

- Artigos multi-idioma com estado por idioma.
- Layouts de portal selecionaveis: landing classica ou documentacao com sidebar.
- Editor com menu slash e suporte nativo a tabelas.
- Criacao de artigos diretamente da visualizacao da categoria.
- Redimensionamento de imagens dentro do editor de artigos.
- Insercao de artigos em conversa com busca estavel em popover.
- Embedding search no Enterprise para busca semantica.
- Geracao assistida de FAQs a partir de PDF com contexto adicional e publicacao seletiva (Enterprise).

### 3.9 Kanban comercial (Mega)

- Funis com etapas configuraveis e etapa padrao.
- Visoes board e list para fluxos distintos de equipe.
- Filtros por inbox, canal, etapa e atividade.
- Filtros por etiquetas de conversa em board/list e nas estatisticas por etapa.
- Gestao de etiquetas direto no card do item com endpoint de API por item.
- Workspace 360 do item: checklist, notas, anexos, ofertas, agentes e atributos.
- Busca remota de conversas/contatos nos seletores de relacoes do item.
- Moeda base configuravel por conta via `accounts.update` (`settings.default_currency`).
- Ofertas custom monetarias com moeda por oferta (`item_details.offers[].currency`) e override sobre a moeda padrao da conta.
- Itens sem ofertas: exibem valor sem moeda e nao entram nos totais monetarios para evitar mistura por fallback.
- Relacao nativa com contato e conversa.
- A sincronizacao do Google Agenda no nivel da conta pode converter itens com data programada/deadline em `CalendarEvent` sem sobrescrever campos Google legacy em `item_details`.
- Os lembretes são avaliados a cada minuto, criam uma única `Notification` idempotente com ator `CalendarEvent` para `created_by_user_id` e reutilizam ActionCable direcionado, Web Push e snooze; emails de convidados nunca definem o destinatário interno.
- Os controles de calendario do item Kanban leem `CalendarEvent`/`ExternalCalendarEvent`, exibem link do Google quando existe e mantem IDs Google legados apenas como fallback.
- Automacoes por etapa e mensagens rapidas.
- Sincronizacao em tempo real com lista de chats e painel de contato.
- O painel de contato/conversa reutiliza os candidatos de agentes do funil e persiste atribuicoes/remocoes pelos endpoints de itens Kanban.
- O bloco Kanban do painel de contato/conversa fica oculto quando o usuario nao tem itens visiveis nem funis disponiveis para criar itens.
- A entrada Kanban do sidebar principal fica oculta para usuarios nao administradores quando eles nao tem funis ativos acessiveis.
- Mudancas nos agentes do funil emitem um evento em tempo real para atualizar sidebar, funis e itens visiveis sem recarregar.
- Um item Kanban pode vincular varias conversas: `conversation_display_id` mantem a conversa principal por compatibilidade e `item_details.conversation_ids` guarda o conjunto completo; visibilidade, filtros, realtime da lista de chats e o bloco Kanban do ContactPanel consideram qualquer conversa vinculada. O seletor de relacionamentos fica limitado aos inboxes do funil e mostra icone de canal/nome do inbox.
- Se uma conversa vinculada for excluida, o item Kanban permanece como historico e a relacao quebrada e limpa.
- Escopo de acesso consistente na API, cache e eventos em tempo real: administradores veem todos os funis e itens; `agent` e a permissao de funcao personalizada `kanban_view` recebem somente os recursos autorizados.
- A permissao de funcao personalizada `kanban_manage` inclui o quadro e o gerenciador; funis que contêm itens autorizados ficam expostos em modo leitura, e somente os atribuidos por `settings.agents` podem ter conteudo e estrutura editados. Nao permite criar, duplicar, excluir, definir o padrao ou alterar `unassigned_visibility`.
- Os itens mantem `created_by_id`, para que o criador sempre preserve a visibilidade. Com uma conversa vinculada valida, o responsavel atual so pode ve-lo se tambem estiver selecionado no funil, e qualquer agente atribuido manualmente ao item pode ve-lo; um vinculo stale fica visivel somente para administrador e criador.
- `unassigned_visibility` aceita `everyone` (valor legado/padrao) e `assigned_only`; define a visibilidade de itens sem atribuicao direta ou de conversas vinculadas sem responsavel.
- Os candidatos em `settings.agents` devem ter acesso a pelo menos uma inbox de `settings.inboxes`; a uniao e recalculada ao alterar inboxes e bloqueia novas atribuicoes invalidas.
- A configuracao global permite leitura a `agent`, `kanban_view`, `kanban_manage` e administradores; criar, editar ou excluir exige administrador. Os endpoints de automacoes globais sao exclusivos de administrador; `kanban_manage` modifica apenas funis atribuidos.

### 3.10 Integracoes e extensibilidade

- Webhooks com payload enriquecido e segredo global HMAC-SHA256.
- Evento de webhook `inbox_updated` para mudancas de estado e desconexao de inboxes.
- Dashboard Apps para extensoes embutidas via iFrame por contexto; usuarios autenticados da conta podem le-los, mas somente administradores podem cria-los, atualiza-los ou exclui-los.
- Dashboard Scripts (Super Admin) para customizacao global sem alterar core.
- Platform Apps para integracoes externas de alto nivel via API.
- Integracoes de negocio: Slack, Linear, Shopify, WooCommerce, Notion, CRM e Google Agenda.
- Google Agenda usa APIs OAuth/config com escopo de conta, `CalendarConnection` selecionado, `CalendarEvent` interno e mapeamento de provedor em `ExternalCalendarEvent`; `settings.import_all_calendars` controla o escopo de entrada separado do `calendar_id` concreto de saida.
- A rota operacional `/app/accounts/:accountId/calendar` le `calendar_events` locais para dia, semana, mes, lista, criar, editar, cancelar, sync ao salvar e sync manual de fallback. `CalendarSync::PollConnectionsJob` roda a cada cinco minutos e importa mudancas Google com `last_polled_at` por calendario salvo em `CalendarConnection.settings`; recorrencias sao expandidas entre um ano atras e cinco anos a frente.
- A navegação, a rota operacional, a ação do compositor e a seção do painel da conversa exigem o feature da conta, credenciais OAuth globais completas e `GoogleCalendarIntegration.connected?` com `CalendarConnection#calendar_id`; os payloads iniciais expõem apenas booleanos de disponibilidade e configuração.
- A visao mensal limita cada celula a dois eventos visiveis para reservar espaco ao controle `+N mais`; o clique direito abre as acoes do evento e cada linha continua abrindo o editor. A cor fica em `metadata.color_id` e a exclusao permanente exige administrador.
- As respostas de `calendar_events` incluem resumos leves de contato, conversa e item Kanban para seletores buscaveis; payloads de edicao enviam `null` para desvincular relacoes.
- O seletor de relacionamentos do calendario busca itens Kanban em toda a conta, sem herdar o funil ativo, e aceita IDs de itens (incluindo o formato `#ID`).
- As tarefas do checklist possuem configuracao propria de sincronizacao com o Google Agenda e calendario de destino; cada tarefa sincronizada e salva como um evento independente vinculado por `checklist_item_id`.
- O agente atribuido ao checklist e adicionado como convidado do Google e recebe o lembrete da plataforma; ao concluir ou excluir a tarefa, o evento e o lembrete pendente sao cancelados.
- O compositor de conversas carrega a conexao da conta e os calendarios gravaveis antes de abrir o `CalendarEventDialog` compartilhado; a acao explicita “Criar e enviar” formata o resultado `saved` com campos localizados e o envia uma unica vez por `createPendingMessageAndSend`, usando `metadata.google_meet_url` sem tentar criar o evento novamente se a mensagem falhar.
- O painel do contato filtra `calendar_events` por `conversation_display_id`, recalcula a cada 30 segundos o avanço Início–Fim para um ponto pulsante verde (<50%), amarelo (50–90%) ou vermelho (≥90%), deixa vencidos opacos, reutiliza `CalendarEventDialog` e consome atualizações de eventos salvos.
- `GoogleCalendar::EventMapperService` mapeia metadata do evento para campos Google de local, convidados, lembretes, recorrencia simples, disponibilidade, visibilidade, permissoes de convidados e Google Meet.
- O editor responsivo usa linhas com icones, seletor de fusos IANA e chips removiveis; a lateral coloca o contexto MEGA vertical abaixo das permissoes dos convidados, com buscas flutuantes e o icone do canal em cada resultado de conversa; persiste destino e URL Meet.
- Google Agenda suporta importacao manual de entrada via `google_calendar_integration/import_events` e backfill Kanban legado via `google_calendar_integration/backfill_kanban`; triggers do Flow Builder ficam diferidos.
- Assets PWA gerados dinamicamente a partir da configuracao global, com fundo de icone configuravel e cache invalidado por logo, cor e timestamp do blob.

### 3.11 Cadastro e onboarding

- Finalizacao guiada do perfil da conta pelo endpoint administrativo dedicado `/api/v1/accounts/:account_id/onboarding`.
- Persistencia do site como URL completa para consumidores posteriores como Help Center e enriquecimento de marca.
- Separacao entre atualizacoes gerais da conta e a conclusao da etapa `account_details`.
- O callback OAuth do Instagram preserva a pista assinada `return_to` para retomar o setup da caixa de entrada quando a autorizacao parte do onboarding.

### 3.12 Seguranca e conformidade

- 2FA/MFA, SAML/SSO, funcoes personalizadas e logs de auditoria.
- Os registros de sessao de usuario suportam uma etiqueta `custom_name` editavel pelo agente; a metadata de IP permanece interna e nao e exposta nos payloads de sessoes do dashboard.
- O estado de dashboard para conta suspensa mantem o widget de suporte visivel e expoe uma acao explicita para contatar o suporte.
- Protecao de licenca Mega em fluxos de deploy.
- Observabilidade de release para rastreabilidade por versao.

## 4. Operacao e validacao

### Paridade da API e coleção Postman

As rotas suportadas em `/api`, `/platform/api` e `/public/api` são comparadas com OpenAPI 3.1 por método e rota normalizada. A validação detecta operações ausentes, obsoletas ou duplicadas; ela não afirma cobertura de testes para cada campo de resposta. `bundle exec rake swagger:build` regenera Swagger e `swagger/postman_collection.json`, organizada em `Account API Token`, `Platform App Token` e `Public / No Token`, com variáveis de credencial independentes.

Checklist recomendado para mudancas funcionais:

1. Validar permissoes por papel e limites de conta.
2. Validar eventos realtime em uso concorrente.
3. Executar testes unitarios do dominio afetado.
4. Executar validacao manual em navegador no fluxo completo.
5. Verificar paridade de i18n em ES, EN e PT-BR para novos textos.

## 5. Referencias tecnicas relacionadas

- [docs/kanban_api_reference_pt_BR.md](../kanban_api_reference_pt_BR.md)
- [docs/chat_rooms_api_reference.md](../chat_rooms_api_reference.md)
- [docs/scheduled_messages_api_reference_pt_BR.md](../scheduled_messages_api_reference_pt_BR.md)
- [docs/platform_banners_api_reference_pt_BR.md](../platform_banners_api_reference_pt_BR.md)
- [docs/whatsapp_voice_calls.md](../whatsapp_voice_calls.md)
