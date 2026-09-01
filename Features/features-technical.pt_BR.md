# MEGA - Detalhe Tecnico de Funcionalidades (PT-BR)

Versao: Enterprise

As gravações do Twilio Voice permanecem anexadas a `Call`; uma configuração explícita da conta habilita sua transcrição idempotente, transmissão da mensagem e indexação na busca.
Ultima atualizacao: 1 de setembro de 2026
Idioma: Portugues (Brasil)

## 1. Objetivo

Este documento descreve como as funcionalidades principais da MEGA estao implementadas do ponto de vista tecnico.
Ele complementa [features.pt_BR.md](features.pt_BR.md), que e voltado para apresentacao comercial.

## 2. Stack base e arquitetura

- Backend principal: Ruby on Rails.
- Frontend dashboard: Vue 3.
- Overlay Enterprise: extensoes e overrides em enterprise.
- Processamento assincrono: Sidekiq para jobs em background.
- Métricas opcionais de filas Sidekiq para o CloudWatch: `ENABLE_SIDEKIQ_CLOUDWATCH` inicia a publicação somente no processo servidor do Sidekiq. Usa o perfil da instância por padrão (ou credenciais dedicadas `SIDEKIQ_CLOUDWATCH_AWS_*`) e publica QueueLatency, QueueSize, EnqueuedJobs e Utilization em um intervalo positivo validado.
- Camada realtime: Action Cable para conversas, salas e quadros.
- Persistencia: PostgreSQL como banco principal.
- Seguranca de API: politicas de permissao e controle por papel.

## 3. Dominios funcionais

### 3.1 Canais de mensagens e voz

- Os identificadores públicos das caixas são resolvidos no frontend por tipo de canal e exibidos junto ao nome na barra lateral, na lista e no cabeçalho de configurações. Os IDs de página do Facebook e de perfil do X são valores opacos de roteamento e, por isso, são excluídos da exibição, embora permaneçam no payload da caixa para operações do provedor. A busca combina correspondências de nome/tipo com os identificadores normalizados visíveis, sem duplicar resultados e preservando a direção de texto misto com `bdi`.
- WhatsApp Cloud API: canal oficial com templates e eventos de entrega; fora da janela de atendimento de 24 horas, o serviço rejeita localmente mensagens livres de automações sem parâmetros de template antes de contatar o provedor.
- Mega Hub para Meta: modo opcional no Super Admin para conectar WhatsApp, Messenger e Instagram usando apps compartilhados do Hub; o bloco de credenciais do Hub é configurado em Super Admin → Mega Hub, e as caixas criadas continuam enviando pelos serviços nativos e recebem eventos reenviados por webhook. A saúde do WhatsApp valida o forward do Hub em vez de comparar o callback da Meta para o Hub com o callback direto do MEGA, e só informa falha de configuração quando confirma que o forward é inválido. A tela final trata o Mega Hub como cadastro integrado e não mostra instruções manuais de URL do webhook nem token de verificação.
- Saúde da conexão do WhatsApp Cloud: falhas de token manual são exibidas sem bloquear o processamento de webhooks recebidos, enquanto o cadastro integrado mantém o fluxo de reautorização.
- A saúde do número do WhatsApp Cloud persiste os dados disponíveis do número quando o enriquecimento opcional do negócio WABA falha, preserva os últimos metadados empresariais e registra o erro de enriquecimento separadamente.
- A Saúde da conta consulta o perfil comercial do WhatsApp sob demanda para caixas Cloud API e o retorna sem persistência. Uma falha nessa consulta é registrada e não oculta os dados principais do número ou do negócio.
- Caixas do WhatsApp Cloud com cadastro integrado podem usar uma migração manual guiada e controlada por feature flag para um aplicativo Meta próprio; o fluxo valida as credenciais de WABA, número e token antes de atualizar a conexão, enquanto o alerta de reautorização permanece visível quando necessário.
- A configuração manual guiada do WhatsApp cria uma nova caixa Cloud a partir de um ID de WABA, ID de número de telefone e token permanente validados. Ela armazena a WABA nas duas chaves de compatibilidade, configura explicitamente o callback no nível do telefone, expõe verificações de callback/assinatura e evita o callback genérico após a criação.
- No Cloud, `whatsapp_embedded_signup_inbox_creation` é o controle único para criar caixas por cadastro integrado, reconfigurá-las proativamente e reautorizá-las. Instalações próprias mantêm `whatsapp_reconfigure` para reconfiguração proativa; o endpoint exige administrador e preserva a recuperação quando a reautorização é necessária.
- O cadastro integrado aceita conclusões de coexistência com WhatsApp Business App sem `phone_number_id`; ele encaminha `is_coexistence` e `is_business_app_onboarding` para que o serviço de autorização configure o canal e os webhooks desse fluxo.
- WhatsApp Evolution, WAHA e Uazapi: provedores alternativos com suporte multimidia e grupos.
- Edições recebidas em grupos via Evolution, WAHA e Uazapi preservam um cabeçalho existente em negrito `número - nome` abaixo do marcador localizado de edição; edições repetidas e corpos já prefixados pelo provedor não duplicam cabeçalhos.
- Os placeholders não suportados do WhatsApp preservam `unsupported_reason`, código e subtipo quando a Meta os fornece. Somente `131060` é classificado como indisponibilidade por coexistência; `131051`, outros tipos e registros antigos usam uma orientação neutra. Mensagens enviadas sem conteúdo enviável ou sem resposta da WAHA são marcadas como falhas, e não como conteúdo recebido não suportado.
- Estado de conexão por provedor: WAHA, Evolution e Uazapi usam suas próprias APIs e webhooks; a validação de assinatura da Meta fica reservada ao WhatsApp Cloud.
- Proxy de sessão do WAHA: a configuração é aplicada por `config.proxy` ao atualizar a sessão, com `server`, usuário e senha opcionais; ela pode ser removida com `proxy: null`.
- Proxy da Uazapi: as configurações da caixa permitem um proxy interno regional com cidade brasileira validada pelo catálogo do provedor, um proxy personalizado sem fallback ou sem proxy; alterar ou remover o proxy aplica o modo correspondente do provedor, e a remoção limpa a preferência regional salva.
- Vinculação WAHA com passkey: detecção proativa da extensão via `WAHA_PASSKEY_CHROME_EXTENSION_ID`, estados `PASSKEY_REQUIRED` e `PASSKEY_CONFIRMATION_REQUIRED` dentro de `session.status`, challenge por `/auth/passkey/challenge`, fluxo temporário por token para asserção, assinatura com extensão de navegador em `web.whatsapp.com` e confirmação manual por código; os GET sem dados pendentes retornam `422`.
- Sincronização global sob demanda para WAHA e Uazapi: jobs Sidekiq com progresso em Redis, janelas de 24h/7d, deduplicação por ids do provedor, reutilização de conversas abertas, download assíncrono de mídia histórica, bloqueio de concorrência por conta e worker dedicado opcional `whatsapp_history_sync` para instalações de alto volume.
- Sincronização por conversa para WAHA e Uazapi: ação manual pelo menu da conversa, com janelas de 24h/7d e deduplicação por ids do provedor.
- Download diferido de mídia de grupos WAHA (lazy media): uma caixa pode ativar `lazy_media_download` para persistir somente a mídia recebida em grupos como anexo pendente (apenas identificadores do provedor em `meta`); um agente baixa sob demanda pelo endpoint de conversa `download_attachment`, que reutiliza o fluxo comprovado em duas etapas metadata-then-binary e anexa o arquivo de forma idempotente. Conversas individuais mantêm o download imediato.
- Reações do WhatsApp: atores do dashboard e tokens de API podem adicionar, substituir e remover uma reação por mensagem preservando ecos do WhatsApp Device.
- Notificame: variante oficial orientada a operacao LATAM.
- Instagram, Facebook, TikTok, Telegram, X, SMS e Email como inboxes.
- A autorização do TikTok é aplicada pela funcionalidade de conta `channel_tiktok`; contas hospedadas sem acesso veem a opção de solicitar suporte e o onboarding exclui o TikTok das sugestões detectadas.
- Processamento de email IMAP com timeout dedicado para evitar jobs travados nas caixas de entrada.
- Diagnóstico de conexão para caixas do Gmail com autenticação IMAP/SMTP XOAUTH2 em tempo real, categorias de erro seguras, datas de atividade recente de entrada/saída e reconexão OAuth exclusiva para administradores.
- Quando mensagens ou conversas são excluídas de caixas Gmail, um job assíncrono busca o RFC `Message-ID` armazenado, resolve os identificadores opacos do Gmail e exclui permanentemente a mensagem ou sequência sem bloquear a exclusão local.
- Inferencia do provedor de email a partir dos registros MX do dominio de cadastro para sugerir integracoes Gmail ou Outlook durante o onboarding.
- Upload de anexos com reconhecimento explicito de arquivos `.pfx` junto aos formatos comuns de midia e documentos.
- API Channel: gateway generico para plataformas proprietarias via API/webhooks.
- Formulário pré-chat do widget: caixas de seleção marcadas como obrigatórias usam a regra de aceitação do formulário, mantendo o envio bloqueado até serem selecionadas; a mensagem localizada de campo obrigatório é preservada.
- Voz Twilio e chamadas WhatsApp Cloud: fluxo WebRTC com linha do tempo unificada; chamadas Cloud feitas de perfis sem conversa resolvem ou criam com segurança o tópico do contato, respeitando a continuidade do inbox e a visibilidade do agente. A permissão de chamada pode usar um modelo aprovado selecionado no ReplyBox ou configurado como padrão do inbox, conserva o WAMID para correlacionar a resposta e registra a mensagem enviada na conversa sem reenviá-la ao provedor. As consultas ao Meta são a fonte de verdade: normalizam e persistem os estados sem permissão, temporário e permanente, e respeitam a ação `start_call` antes de iniciar uma chamada; cada alteração é registrada como atividade, com a data de vencimento recebida para permissões temporárias. Cliente e servidor impedem uma segunda chamada ativa por agente, inclusive entre abas. Os candidatos do inbox são determinados pelas regras padrão de atribuição —capacidade, equipe e overflow— e quem já está em chamada é excluído; um administrador online que ativou notificações entra apenas como fallback quando não resta um agente elegível. Enquanto uma chamada Cloud está sendo aceita, conectada ou ativa, a interface e o modelo rejeitam alterações de agente e equipe; uma chamada que apenas toca continua podendo ser reatribuída e a alteração volta a estar disponível após o encerramento. Os controles, as solicitações de permissão, o início e os webhooks de chamadas são desativados para canais Cloud marcados como coexistência com o WhatsApp Business App, porque as chamadas continuam no aplicativo WhatsApp Business. Os relatórios Twilio normalizam dados a partir do modelo Call, as gravações nativas opcionais exigem aceite do custo de storage e as gravações aparecem nas conversas e no relatório de chamadas.
- Controle de transcricao de audio: GPT-4o Mini Transcribe por padrao para notas de voz com Whisper disponivel como override por conta; as gravacoes mantem flags por conta para habilitacao geral e comportamento por provedor (WhatsApp Cloud e WaVoIP), normalizacao de audio, diarizacao por turno, transcricao fiel com GPT-4o Transcribe, rotulos baseados no nome do contato/agente atribuido e reprocessamento manual pelo menu contextual de mensagens de audio sem texto. As transcricoes armazenadas participam do OpenSearch, do fallback GIN/SQL, dos resultados globais de conversas e da busca de mensagens dentro de uma conversa, preservando os escopos de permissao e filtros existentes.
- WaVoIP com persistencia de sessao por inbox e reaproveitamento de credenciais conforme o papel do usuario.

### 3.2 Nucleo de conversas

- As solicitacoes de transcricao por email no widget desabilitam o botao durante o envio e por 15 segundos apos um envio bem-sucedido, evitando solicitacoes repetidas e mantendo a nova tentativa imediata apos uma falha.
- A visibilidade do feedback CSAT e armazenada por inbox em `csat_config.hide_feedback_from_agents`. Os serializadores de mensagens do dashboard e o Action Cable removem apenas `feedback_message` para usuarios da conta que nao sao administradores, enquanto as avaliacoes, os dados persistidos e os payloads de administradores e clientes permanecem inalterados.
- As mensagens excluidas podem reter o texto original e os anexos para agentes por meio de `inboxes.show_deleted_message_placeholder`; a API publica, os payloads do widget e os broadcasts do Action Cable destinados ao contato substituem `content` e `processed_message_content` pelo aviso de exclusao, omitem `content_attributes.original_content` e `translations`, e expoem uma lista vazia de anexos sem alterar o registro persistido.
- O endpoint de mensagens do widget retorna `403 Forbidden` para envios de texto e anexos a uma conversa resolvida quando `inboxes.allow_messages_after_resolved` é falso. Essa proteção no servidor também cobre novas tentativas de mensagens com falha e mantém a conversa resolvida sem alterações.
- Modelo de status: open, pending, resolved, snoozed.
- Os timestamps relativos do dashboard usam `exactTimestamp` em um tooltip com atraso, exibindo data e hora completas; `TimeAgo` mostra criação e última atividade em linhas separadas.
- Modelo de prioridade: tratamento de urgencia por conversa.
- Participantes: colaboracao multiagente na mesma thread.
- API de atributos personalizados: `POST .../custom_attributes` mantém a substituição como padrão e aceita `merge=true` para atualizar apenas as chaves recebidas; `POST .../destroy_custom_attributes` remove chaves específicas e retorna os atributos restantes.
- Execução de macros e atributos obrigatórios: o editor de resposta oferece um seletor com `#`, enquanto a barra de comandos mostra **Executar uma macro** somente em rotas de conversa ativas com a função de macros habilitada; ambos usam a mesma ordem persistida da barra lateral. As três superfícies compartilham a execução, detectam `resolve_conversation` e `change_status` para resolvida, solicitam e persistem valores ausentes antes da execução e podem continuar sem resolver quando o diálogo é fechado. O overlay de `Macros::ExecutionService` também bloqueia a resolução direta enquanto faltarem valores de definições obrigatórias vigentes; checkbox `false` conta como preenchido e valores nulos como ausentes.
- Rascunhos e fixadas: continuidade de trabalho por agente.
- Filtros avancados e visoes personalizadas: segmentacao para alto volume.
- Ordenacao dedicada por unread na lista de conversas.
- Filtros dedicados no sidebar: unread, mentions, participating, groups e unattended na navegacao de conversas.
- Contadores reativos no sidebar: unread por tipo de conversa e mentions via notification_type=conversation_mention.
- A interface legada de histórico e a rota `/notifications` são removidas, enquanto `inbox_view` permanece desabilitado. As notificações persistidas continuam alimentando popups realtime, contadores do sidebar e reconciliação após reconexão. Calendário usa seu payload Push especializado; `kanban_note_agent_assigned`, `kanban_stage_automation`, `kanban_checklist_due_date` e `account_task_due` usam um payload operacional separado com URLs diretas e sem entrega por e-mail.
- Assignment V2: distribuicao inteligente com capacidade e regras.
- Os inboxes expoem `auto_assign_on_agent_reply` para manter conversas nao atribuidas sem responsavel quando um agente envia uma mensagem de saida.
- Usuários com várias contas mantêm um único seletor de avatar, mas suas operações de upload e remoção atuam sobre o vínculo `AccountUser` ativo. Os payloads de agentes e mensagens priorizam esse avatar e usam o avatar global de `User` como fallback; o comportamento de usuários com uma única conta continua global e nenhum permissionamento ou toggle de política é adicionado.
- Equipes: `icon` e `icon_color` sao persistidos em `teams`, expostos pela API/model JSON e incluidos nos payloads realtime para listas e seletores de atribuicao.
- SLA Enterprise: `AppliedSla` expoe prazos FRT/NRT/RT calculados no backend; quando a politica usa horario comercial, `Sla::BusinessHoursService` consome a configuracao de working hours do inbox e a resposta JSON entrega `sla_*_due_at` ao dashboard. Ao resolver uma conversa, `sla_completed_at` e registrado e congela a duracao exibida dos descumprimentos FRT/NRT/RT; SLAs historicos sem essa marca continuam visiveis como descumprimentos estaticos. Conversas com contato bloqueado rejeitam nova atribuicao de SLA, sao excluidas de processamento/relatorios e limpam `sla_policy_id`, `applied_sla` e `sla_events` dos payloads enquanto seguirem bloqueadas.
- Drilldown de relatorios V2: `/api/v2/accounts/:account_id/reports/drilldown` retorna as conversas, mensagens ou eventos que compoem uma barra do grafico; `V2::Reports::DrilldownBuilder` valida metrica, bucket, permissao de administrador, paginacao, filtros por conta/inbox/agente/equipe/etiqueta, horario comercial e serializacao da ultima mensagem, com rate limit dedicado no Rack::Attack.
- Respostas prontas com anexos reutilizaveis tambem nos fluxos de nova conversa.
- O seletor de respostas prontas e teletransportado e ancorado ao cursor, carrega a lista da conta pelo cache IndexedDB endurecido, filtra atalhos/conteudo localmente, reconcilia invalidacoes em tempo real, mostra conteudo renderizado compativel com o canal e preserva placeholders Liquid sem valor para avaliacao no backend.
- Editor de resposta com upload de imagens inline em Email e Widget Web, redimensionamento por ProseMirror e renderizacao segura de `cw_image_width`/`cw_image_height`.
- A resolucao de `reply_to` no WhatsApp respeita `conversation_history` buscando identificadores citados em conversas anteriores do mesmo contact inbox, sem ampliar a busca para todas as mensagens da conta. Em coexistencia, tambem vincula WAMIDs de escopo de telefone e BSUID que compartilham um unico token decodificado; identificadores malformados ou ambiguos permanecem sem vinculo.
- Fluxo de desligamento de agentes com revisao previa das conversas atribuidas e opcao de desatribuir ou reatribuir em lote respeitando acesso por inbox/equipe.
- Convites de agentes reservam atomicamente a capacidade diária de e-mails no Redis antes de enfileirar a mensagem; um limite esgotado reverte apenas aquele convite e responde HTTP 429, enquanto a inclusão em massa continua adicionando usuários existentes.

### 3.3 Comunicacao interna e salas

- Chat Rooms permanece como dominio proprio sobre a base existente: `chat_rooms`, `chat_room_members` e `chat_room_messages`.
- Os nomes das salas preservam as maiúsculas informadas; `chat_rooms` aplica unicidade por conta sem diferenciar maiúsculas por meio de um índice único `account_id, LOWER(name)`.
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

- Regras com espera persistem uma execução pendente reclamada por regra, conversa e episódio de estado. O editor preserva as condições estruturais da espera e aceita condições adicionais unidas com `AND`; um worker agendado revalida a feature flag, a regra e todas as condições antes de executar. Mudanças de status e respostas invalidam o episódio correspondente.

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
- Novas conversas e campanhas sem remetente de um Agent Bot ativo ficam pendentes com o bot como proprietário; atribuições humanas explícitas são preservadas, e o handover, a abertura humana ou a desconexão do bot limpam sua propriedade. Dialogflow, Captain e destinos ignorados não recebem um proprietário Agent Bot.
- O escopo compartilhado `Conversation.unassigned` exige que tanto `assignee_id` quanto `assignee_agent_bot_id` sejam nulos, portanto conversas de bot não afetam a lista nem o contador da fila humana sem atribuição.
- A expiração de sessão de Webhook usa o handover canônico: abre a conversa, limpa a propriedade do bot e habilita a atribuição automática humana somente nessa transição. Sem agente elegível, a conversa permanece aberta e sem atribuição com as tentativas limitadas existentes.
- O ReplyBox detecta a propriedade `AgentBot` em conversas pendentes, força o modo efetivo `NOTE` sem sobrescrever rascunhos de resposta, e o banner para assumir reabre e atribui a conversa ao agente atual, atualizando também o tipo de responsável local.
- Typebot estendido com comandos MEGA_CMD para atribuicao de agente/equipe.
- Typebot ignora reacoes de WhatsApp para evitar inicios ou mensagens artificiais.
- Assinaturas de webhook por canal para validar autenticidade de eventos de saida.

### 3.5 IA Captain

- Provedores suportados: OpenAI, Anthropic, Google, Azure OpenAI, Bedrock, DeepSeek.
- Assistants: configuracao por inbox com instrucoes e contexto. `config.auto_resolve_mode` e persistido por assistente como `evaluated`, `legacy` ou `disabled`; assistentes existentes sem esse valor usam o modo da conta como compatibilidade. Com o Captain V2, `config.auto_resolve_after` aceita de 5 a 1.440 minutos e e normalizado em incrementos de cinco, enquanto `send_inactivity_resolution_message` controla a mensagem publica. Uma árvore validada e opcional de condições de público e `response_window` (`always`, `business_hours` ou `outside_business_hours`) definem a elegibilidade ao criar ou reabrir conversas; as que já estão pendentes continuam sem interrupção. A API mescla com seguranca as atualizacoes de configuracao e serializa os valores efetivos.
- A reconciliação de faturamento cloud ativa `captain_integration_v2` para todo plano que não seja o padrão e o desativa para o plano padrão configurado. Ela não depende de um atributo de rollout por conta; o runtime do Captain V1 e a flag de recurso continuam disponíveis.
- Exclusividade de bots: `InboxBotStatus` identifica Agent Bots ativos e Dialogflow como bots externos; o Captain não agenda respostas nem resolução automática para esses inboxes.
- Visao geral do assistente: os endpoints Enterprise legados de estatisticas, drilldown e resumo cacheado continuam baseados em `Captain::AssistantStatsBuilder`, `Captain::AssistantStatsWindow`, `Captain::AssistantDrilldownBuilder` e `Captain::OverviewSummaryService`. A flag local `captain_overview_v2` seleciona uma interface redesenhada e opcional que consome os builders dedicados de resultados, fluxo e tendencia de resolucao; a tendencia inclui taxas alinhadas do periodo atual e anterior, enquanto o CSAT apenas humano indisponivel permanece nil em vez de uma pontuacao falsa. `overview_summary` gera no servidor ate tres insights localizados e arredondados, ignora relatorios sem atividade e compartilha no Redis um cache bem-sucedido de uma hora por conta, versao do assistente, intervalo, fuso horario e idioma. O tempo economizado estimado e derivado das respostas publicas do assistente usando uma suposicao fixa de 2 minutos de esforco do agente por resposta.
- O roteamento de modelos Captain separa recursos de cliente e internos no Super Admin. O avaliador interno `conversation_completion` aceita modelos OpenAI compatíveis; sua rota resolve o override da conta, depois o modelo da instalação auto-hospedada e por fim o padrão do YAML. As preferências do Captain para clientes continuam expondo somente recursos de cliente.
- Editor de resposta do Copilot: mede as sugestões renderizadas após a atualização do DOM e cresce temporariamente para exibi-las, com limite de 350 px. O redimensionamento manual mantém prioridade e é restaurado quando a sugestão fecha; os estados de carregamento e sugestão fazem cross-fade no mesmo lugar.
- Sugestões de resposta do Copilot: uma solicitação explícita valida o acesso do agente à conversa e uma última mensagem pública recebida. Um job dedicado usa o prompt, FAQs, citações e somente custom tools GET do assistente, sem cenários ou handoff; ele revalida acesso e atualidade antes de persistir, descarta rascunhos obsoletos e consome crédito apenas por uma resposta válida salva.
- Sugestões de FAQ por conversa: um job de baixa prioridade com mutex extrai apenas mensagens públicas de clientes e agentes humanos junto com o contexto do negócio, rejeita conversas inadequadas e agrupa observações semanticamente equivalentes por assistente e idioma; FAQs aprovadas e sugestões descartadas impedem novos duplicados.
- Revisão de sugestões de FAQ: a API Enterprise lista e pré-visualiza apenas fontes acessíveis ao agente atual, permite editar, aprovar ou descartar sugestões abertas e bloqueia revisões contra aprovações simultâneas. A aprovação cria uma FAQ aprovada e preserva suas observações de origem.
- Detalhes da geração: `GET /api/v1/accounts/:account_id/captain/agent_sessions/:message_id` no Enterprise autoriza a conversa da mensagem, hidrata citações e títulos de cenários e alimenta o popover da mensagem Captain. As sessões são armazenadas por mensagem; uma sessão de transferência é associada à sua nota privada não vazia. O modelo e os créditos são exibidos apenas para superadministradores ou em desenvolvimento.
- Citações confiáveis do Captain V2: `faq_lookup` retorna índices locais tipados sem URLs; o agente principal continua sem `response_schema` e emite marcadores `[[citation:N]]` que o servidor converte em partes persistidas, filtra pelo mapa da execução e renderiza apenas documentos HTTP(S) públicos do assistente. Credenciais, destinos privados, PDFs e parâmetros assinados são rejeitados; `faq_ids` preserva resultados recuperados, enquanto `used_faq_ids` e `cited_document_ids` guardam apenas seleções válidas. O histórico reutiliza texto limpo e sessões legadas com as novas colunas nulas continuam sendo hidratadas por `faq_ids`.
- Captain Documents: upload, indexacao e auto-sincronizacao por plano com jitter, fila purgable, limites configuraveis por conta e globais e uma vista de detalhes com conteudo rastreado, metadados da fonte, quantidade de FAQs geradas e uso em conversas exclusivo para administradores.
- Analitica de uso de conhecimento: `Captain::ConversationUsageBuilder` calcula conversas ativas distintas a partir de sessoes do assistente com resposta entregue (`credits_consumed > 0`), usando indices GIN em `document_ids` e `used_faq_ids`; pagina drilldowns em 25 registros, exclui handoffs e conversas excluidas, permite ordenar documentos por uso e expoe o uso de FAQs criadas por usuarios apenas a administradores.
- Captain Scenarios: regras de ativação e prioridade; as APIs de gerenciamento retornam registros ativados e desativados, enquanto apenas os ativados são executados. A API preserva `tools` enviados explicitamente, normaliza IDs escalares ou metadados `{ id }`, aceita referências salvas a ferramentas personalizadas desativadas e mantém referências `tool://` quando o campo é omitido. O Account MCP publica schemas específicos para criar e atualizar cenários.
- Captain Custom Tools: integrações HTTP com GET, POST, PUT, PATCH e DELETE; aceitam fragmentos JSON Schema para parâmetros complexos e o Account MCP publica contratos diretos para listar, criar, consultar, atualizar, excluir e testar tools personalizadas. A resposta de detalhe informa quantos cenários ativados usam uma ferramenta, para que o dashboard avise antes da desativação; ferramentas desativadas são excluídas da execução.
- Runtime de tools Captain: preserva integralmente o `inputSchema` de cada servidor MCP, encaminha objetos e arrays sem convertê-los em texto, exclui servidores desabilitados ou desconectados, atualiza a cada 10 minutos os catálogos conectados obsoletos e limita cada solicitação a 128 tools incluindo handoffs. Uma falha transitória de conexão preserva o último catálogo utilizável e mantém o servidor elegível para nova tentativa; erros permanentes não anunciam um catálogo obsoleto como conectado. No Playground V1 e V2 não existe seleção direta por `@` ou `tool://`. V1 testa o assistente legado base sem tools MCP diretas; V2 mantém as tools normais do assistente principal, executa os handoffs e carrega em cada agente de cenário somente suas tools atribuídas, como em uma conversa real. As referências `tool://` na configuração de cenários continuam suportadas. O proxy aceita objetos JSON e strings contendo objetos JSON, mas rejeita JSON inválido ou valores que não sejam objetos em vez de esvaziá-los silenciosamente.
- MCP nativo por conta: endpoints dedicados por slug em /mcp/:account_id/:slug. As execuções do Captain para um MCP nativo levam uma prova assinada de uso único vinculada à conta, assistente, servidor, endpoint, tool e argumentos; o handshake permanece neutro e chamadas MCP externas mantêm sua identidade normal.
- Os diagnósticos do cliente MCP usam nível INFO para impedir que o logger DEBUG do transporte exponha cabeçalhos de autorização ou provas de execução.
- Conexões nativas para a própria instância podem usar `MCP_INTERNAL_BASE_URL`; desenvolvimento usa por padrão `MCP_INTERNAL_PORT`/3000 e nunca herda o `PORT` por processo do worker. Somente a origem é substituída, preservando a rota da conta e a assinatura da solicitação enquanto evita timeouts de hairpin pelo DNS público.
- Um `conversation_message_send` nativo encerra o turno Captain somente com um resultado estruturado bem-sucedido que confirma conversa ativa, mensagem pública de saída e remetente Captain. Seu marcador de ciclo de vida, consumo e evento de conclusão são idempotentes; turnos obsoletos são descartados antes do efeito MCP.
- O endpoint MCP POST mantém JSON-RPC por `application/json` e aceita uma extensão `multipart/form-data`: `payload` contém a solicitação JSON-RPC completa e `attachments[]` leva os arquivos locais.
- Uploads multipart são restritos a `conversation_message_send`, seu alias legado e `outbound_messages_create`; respeitam `MAXIMUM_FILE_UPLOAD_SIZE`, com 15 anexos combinados para conversas e exatamente um para outbound.
- Multipart é uma extensão HTTP da Mega que exige suporte explícito do cliente; clientes MCP padrão limitados a JSON não a utilizam automaticamente.
- O handshake JSON de upload direto da conversa aceita o token API do usuário efetivo do MCP, valida conta e conversa pelo stack API/Pundit e devolve o destino assinado do Active Storage sem exigir CSRF do navegador.
- `outbound_messages_create` expõe no MCP o contrato universal completo: `body` preserva inbox, uma identidade do destinatário, texto/mídia/template e um signed blob; `idempotency_key` é encaminhado apenas como `Idempotency-Key`. A mídia aceita exatamente uma fonte entre signed ID, multipart, `file` com URL HTTPS temporária e `file_base64`; em mensagens de template, essa fonte é atribuída a `template.parameters.header.media_file` em vez de um anexo comum.
- O descritor `_meta["openai/fileParams"]` permite que o ChatGPT entregue `file.download_url` e `file.file_id`; Claude e outros clientes podem usar o mesmo descritor, multipart ou o fallback JSON base64. As URLs passam pelo `SafeFetch` com proteção SSRF e limite de tamanho; blobs temporários são removidos se a API falhar.
- O serviço outbound verifica se cada signed ID de mídia resolve para um blob persistido, com tamanho positivo e objeto existente no armazenamento. Uma referência inválida, expirada ou sem bytes retorna `422 invalid_attachment` antes de criar a mensagem ou chamar o provedor.
- OAuth MCP: metadata .well-known, register, authorize, token, refresh token e PKCE.
- Autenticacao dupla: Bearer OAuth ou Api-Access-Token estatico.
- Catalogo MCP curado para uso cotidiano: ferramentas com nomes estaveis por dominio (conversations, contacts, inboxes, help center, reports, kanban e outros).
- Tools MCP publicadas: base (account_context, account_actions_list, account_action_call) + catalogo curado; inclui agendamento de mensagens, tarefas, modelos, campanhas, SLA, politicas, calendario, relatorios, Captain, notificacoes, chat interno e o ciclo completo do Help Center; nao publica tools de importacao nem exportacao de dados; dinamicas explicitas via allowed_tools.
- Auto-resolve mode: evaluated, legacy ou disabled por assistente. O modo avaliado envia ao avaliador o status da conversa e o conteúdo rotulado das mensagens não privadas; os caminhos de resolução e handoff bloqueiam e recarregam a conversa antes da transição, criam mensagens na transação e emitem eventos somente após sucesso. Transferências e acompanhamentos pendentes permanecem abertas.

### 3.6 CRM e gestao de contatos

- Atributos personalizados por tipo de dado e uso em automacoes.
- Visibilidade por papel para atributos sensiveis (Enterprise).
- Etiquetas em contatos e conversas.
- O submenu de etiquetas do menu de contexto das conversas usa busca aproximada com `picoSearch`, mostra primeiro as etiquetas atribuidas sem alterar a ordem de origem de cada grupo e permite selecoes repetidas sem tirar o foco da busca. Consultas em branco mostram todas as etiquetas e o menu de contexto so fecha quando o foco sai dele.
- Empresas agrupadas por dominio com timeline unificada.
- A entrada do sidebar de Empresas e sua autorizacao CRUD estao disponiveis para administradores, agentes padrao e funcoes personalizadas com a permissao `companies_manage`.
- Os payloads de contato expõem `company_id` quando Companies esta habilitado; atualizacoes de contato podem atribuir ou limpar a empresa e mantem `additional_attributes.company_name` sincronizado.
- Importacao e exportacao de contatos disponiveis para administradores e papeis Enterprise com permissao `contact_manage`.
- A exportacao CSV de contatos usa `CSVSafe` para prefixar valores iniciados por caracteres de formula e impedir sua execucao em planilhas.
- A importação do Intercom é exclusiva para administradores e protegida pela feature `data_import`; credenciais e mapeamentos persistentes são armazenados por conta.
- Páginas de contatos e conversas são processadas por jobs Sidekiq, com registros idempotentes de itens/mapeamentos, logs de ignorados/erros, execuções retomáveis e caixas de entrada API por origem.
- Importações inativas por 15 minutos podem ser retomadas por um endpoint autorizado da conta; a nova tentativa bloqueia a conta e a importação, alterna o identificador da execução e preserva cursor, estatísticas e erros registrados.
- Bloqueio ativo no WhatsApp para descartar mensagens recebidas de contatos bloqueados.

### 3.7 Campanhas

- Ongoing campaigns para widget/live chat.
- One-off campaigns para WhatsApp, SMS e API Channel.
- Construtor de templates Meta com ciclo de aprovacao e sincronizacao.
- O endpoint cache-only do inbox lista templates de WhatsApp nativo e Twilio, aplica a chave de nome exato de cada provedor e expõe a última tentativa de sincronização sem consultar a Meta nem a Twilio.
- Controle de velocidade, rotacao multi-inbox e metricas de execucao.

### 3.8 Help Center

- Artigos multi-idioma com estado por idioma.
- Edições de titulo e conteúdo de artigos publicados são mantidas em colunas de rascunho, com fluxos de revisão, publicação e descarte que preservam a versão visível até a publicação.
- Layouts de portal selecionaveis: landing classica ou documentacao com sidebar.
- A análise do portal é armazenada em `portal.config.analytics`; apenas administradores podem atualizar os identificadores permitidos, validados pelo modelo antes de renderizar os scripts públicos de rastreamento.
- Conteúdo recomendado por localidade é persistido em `portal.config.popular_content`, com listas ordenadas limitadas a 3 categorias e 6 artigos; registros excluídos e artigos não publicados são omitidos, preservando o fallback por popularidade.
- Editor com menu slash, tabelas nativas, envios de imagens em segundo plano (progresso, cancelamento e nova tentativa) e envio de MP4 ou URLs de vídeo compatíveis; a mídia mantém sua posição durante o envio e as dimensões do vídeo persistem no editor e no portal público.
- O menu slash do editor de artigos expõe `horizontalRule`, que insere o nó horizontal existente do ProseMirror e move o cursor para o parágrafo seguinte.
- Quando a seleção do ProseMirror está dentro de uma tabela, o menu slash filtra comandos de bloco que as células Markdown não conseguem persistir e mantém apenas formatação inline; as setas e Ctrl+N/P ficam sob controle do menu enquanto houver opções.
- Criacao de artigos diretamente da visualizacao da categoria.
- Redimensionamento de imagens dentro do editor de artigos.
- Insercao de artigos em conversa com busca estavel em popover.
- Embedding search no Enterprise para busca semantica.
- Geracao assistida de FAQs a partir de PDF com contexto adicional e publicacao seletiva (Enterprise).

### 3.9 Kanban comercial (Mega)

- Funis com etapas configuraveis e etapa padrao.
- Visoes board e list para fluxos distintos de equipe.
- `ListTab` consome `GET /kanban_items` em páginas de 30 cards, substitui o estado na primeira página e adiciona itens únicos nas seguintes; ao trocar de funil, reinicia cards e metadados antes de solicitar a nova página inicial.
- `GET /kanban_items/report_export` usa o escopo de políticas Kanban e os filtros do relatório sem paginação. Ele emite CSV UTF-8 com BOM e linhas CRLF por Ruby CSV, cabeçalhos/prioridades localizados, nomes configurados de etapa e moeda explícita do item antes da moeda da conta.
- Filtros por inbox, canal, etapa e atividade.
- Filtros por etiquetas de conversa em board/list e nas estatisticas por etapa.
- O formulário compartilhado de criação carrega as etiquetas da conta e envia os títulos selecionados em `kanban_item.labels`; o endpoint de criação as atribui ao novo item antes da única persistência, sem alterar as etiquetas da conversa vinculada. O card mantém o endpoint de gestão de etiquetas por item.
- Workspace 360 do item: checklist, notas, anexos, ofertas, agentes e atributos.
- Notas longas do Kanban usam um diálogo de detalhes com Markdown renderizado, rolagem limitada ao viewport, quebra forçada para texto sem separadores, anexos e uma ação de edição direta condicionada às permissões.
- Busca remota de conversas/contatos nos seletores de relacoes do item.
- Moeda base configuravel por conta via `accounts.update` (`settings.default_currency`).
- Os consumidores monetários ativos resolvem a moeda pelo helper/composable compartilhado com prioridade oferta → item → conta → locale; valores históricos anterior/novo são formatados separadamente e valores zero permanecem visíveis.
- `funnels/:id/stage_stats` preserva `count` e `total_value` e adiciona `value_totals` por etapa (`currency` ou `label`, código, total e contagem única de itens) sobre todo o policy scope filtrado; `KanbanColumn` prioriza esse agregado completo, usa agrupamento local apenas como fallback de compatibilidade e expõe um tooltip acessível com tokens semânticos.
- Ofertas custom monetarias com moeda por oferta (`item_details.offers[].currency`) e override sobre a moeda padrao da conta.
- Itens sem ofertas: exibem valor sem moeda e nao entram nos totais monetarios para evitar mistura por fallback.
- Relacao nativa com contato e conversa.
- A sincronizacao do Google Agenda no nivel da conta pode converter itens com data programada/deadline em `CalendarEvent` sem sobrescrever campos Google legacy em `item_details`.
- Os lembretes são avaliados a cada minuto, criam uma única `Notification` idempotente com ator `CalendarEvent` para `created_by_user_id` e reutilizam ActionCable direcionado, Web Push e snooze; emails de convidados nunca definem o destinatário interno.
- Os controles de calendario do item Kanban so sao montados quando a conta tem `GoogleCalendarIntegration.connected?` e um `CalendarConnection#calendar_id`; entao leem `CalendarEvent`/`ExternalCalendarEvent`, exibem link do Google quando existe e mantem IDs Google legados apenas como fallback.
- Automacoes por etapa e mensagens rapidas.
- Regras temporizadas `send_message` capturam o ID da conversa principal e o ID da última mensagem recebida quando são agendadas. `StageTimeAutomationJob` revalida a entrada na etapa e a regra, enquanto `KanbanItems::StageFollowUpService` bloqueia o item, cancela após uma nova resposta do contato e desduplica com uma chave de item/regra/entrada nos atributos da mensagem. Texto e multimídia persistida no funil usam `Messages::MessageBuilder`; o editor Woot compartilhado expõe as variáveis Liquid do ReplyBox e o concern `Liquidable` da mensagem as resolve com a conversa de destino. Templates aprovados são exibidos e aceitos apenas para inboxes configurados `whatsapp_cloud`, preservando seus `template_params` por inbox e a restrição existente de 24 horas.
- As etapas de entrada persistem `ignore_group_conversations`; quando ativado, `AutoCreateItemJob` não cria itens para conversas cujo `contact_inbox.source_id` termina em `@g.us`, sem alterar etapas legadas baseadas em condições.
- A entrega automática de modelos da etapa é identificada por `kanban_item_id` e pelo ID estável do modelo nos atributos de conteúdo da mensagem de saída. O editor de modelos habilita o seletor padrão de variáveis ao digitar `{{`; `Liquidable` resolve valores como `{{contact.name}}` ao criar a mensagem de saída. Modelos existentes enviam uma vez por item por padrão; `resend_on_entry` habilita o envio em cada entrada que atender às condições, enquanto mensagens rápidas manuais não consultam esse histórico.
- As regras de etapa `notify_team` resolvem membros das equipes selecionadas e agentes atualmente atribuídos ao item na execução, excluem o usuário que realizou a movimentação, desduplicam usuários e criam notificações em tempo real `kanban_stage_automation` por usuário. Um banner não bloqueante do Kanban mostra um alerta diretamente ou agrupa vários em uma lista expansível com descarte individual ou em massa; o envio por email fica intencionalmente excluído.
- Uma tarefa pendente de checklist com data limite agenda um alerta interno para seu agente atribuído. O job verifica se tarefa, responsável e data continuam atuais antes da entrega, bloqueia o item Kanban para evitar alertas concorrentes duplicados e só recria um alerta dispensado após o intervalo configurado no funil enquanto a tarefa permanecer pendente.
- Sincronizacao em tempo real com lista de chats e painel de contato.
- `GET /kanban_items?contact_id=<id>` preserva o scope autoritativo da policy Kanban, resolve o vínculo por todos os display IDs de conversas relacionadas e filtra itens abertos antes da paginação somente para funis com `settings.contact_panel_contact_wide_items` habilitado. A opção é falsa por padrão; o ContactPanel combina o resultado expandido com `currentChat.kanban_items` e o atualiza com eventos Kanban.
- O painel de contato/conversa reutiliza os candidatos de agentes do funil e persiste atribuicoes/remocoes pelos endpoints de itens Kanban.
- O quadro abre a conversa vinculada pelo ícone de canal sem reinicializar os dados do quadro. No mobile, o detalhe do item separa o conteúdo comercial do perfil/acordeoes e reutiliza os diálogos de status, movimento e agentes do ContactPanel.
- O bloco Kanban do painel de contato/conversa fica oculto quando o usuario nao tem itens visiveis nem funis disponiveis para criar itens.
- A entrada Kanban do sidebar principal fica oculta para usuarios nao administradores quando eles nao tem funis ativos acessiveis.
- Mudancas nos agentes do funil emitem um evento em tempo real para atualizar sidebar, funis e itens visiveis sem recarregar.
- Um item Kanban pode vincular varias conversas: `conversation_display_id` mantem a conversa principal por compatibilidade e `item_details.conversation_ids` guarda o conjunto completo; visibilidade, filtros, realtime da lista de chats e o bloco Kanban do ContactPanel consideram qualquer conversa vinculada. O seletor de relacionamentos fica limitado aos inboxes do funil e mostra icone de canal/nome do inbox.
- `AutoCreateItemJob` garante um único item aberto por contato e funil: serializa o processamento com o bloqueio do contato, reutiliza o item aberto mais antigo e adiciona a nova conversa quando seu inbox pertence ao funil. Contatos distintos não são inferidos por seus dados, os funis são avaliados de forma independente e itens `won`/`lost` permitem uma nova oportunidade.
- Ao abrir uma conversa pelo drawer do Kanban, `ConversationSidebar` repassa `hidePreviousConversations` ao `ContactPanel` para ocultar o acordeão de conversas anteriores; o painel padrão de conversa mantém esse acordeão. O cartão deduplica as conversas serializadas por `inbox.channel_type` e, quando ausente, por `inbox_id`, para exibir um ícone por canal e filtra o seletor para o canal do ícone clicado.
- Se uma conversa vinculada for excluida, o item Kanban permanece como historico e a relacao quebrada e limpa.
- Escopo de acesso consistente na API, cache e eventos em tempo real: administradores veem todos os funis e itens; `agent` e a permissao de funcao personalizada `kanban_view` recebem somente os recursos autorizados.
- O administrador atual pode se atribuir a qualquer item, individualmente ou em massa, e se remover individualmente, mesmo sem pertencer a `settings.agents` ou aos inboxes do funil; essa exceção não permite atribuir outros usuários inelegíveis.
- A permissao de funcao personalizada `kanban_view` pode operar itens visiveis; `kanban_manage` tambem cria funis e fica adicionado a `settings.agents` do funil criado. Somente os funis atribuidos podem ter conteudo e estrutura editados; nao permite excluir, definir o padrao ou alterar `unassigned_visibility`.
- Os itens mantem `created_by_id`, para que o criador sempre preserve a visibilidade. Com uma conversa vinculada valida, o responsavel atual so pode ve-lo se tambem estiver selecionado no funil, e qualquer agente atribuido manualmente ao item pode ve-lo; um vinculo stale fica visivel somente para administrador e criador.
- `unassigned_visibility` aceita `everyone` (valor legado/padrao) e `assigned_only`; `everyone` concede a todos os agentes do funil visibilidade sobre todos os seus itens, inclusive os atribuídos, enquanto `assigned_only` preserva o escopo dos agentes autorizados.
- Qualquer membro da conta com acesso ao Kanban pode ser adicionado a `settings.agents`, independentemente de `settings.inboxes`; uma função personalizada requer `kanban_view` ou `kanban_manage`. Com inboxes configuradas, novas atribuições manuais a itens continuam exigindo acesso a pelo menos uma delas; ao mover um item, seus agentes atribuídos são incluídos automaticamente no funil de destino sem alterar suas permissões de inbox.
- A configuracao global permite leitura a `agent`, `kanban_view`, `kanban_manage` e administradores; criar, editar ou excluir exige administrador. Os endpoints de automacoes globais sao exclusivos de administrador; `kanban_manage` modifica apenas funis atribuidos.

### 3.10 Integracoes e extensibilidade

- API universal de saída: `POST /api/v1/accounts/:account_id/outbound_messages` exige `api_access_token` e autorização sobre o inbox; aceita exatamente um entre `phone_number`, `email`, `contact_id` ou `source_id`, resolve ou cria contato/contact-inbox/conversa e entrega texto, um anexo ou um template de WhatsApp ao `Messages::MessageBuilder` e `SendReplyJob`. Para templates, renderiza o BODY aprovado sincronizado com suas variáveis antes de persistir a mensagem, para que o dashboard e os webhooks exponham o conteúdo enviado. Templates de canais WhatsApp nativos (exceto Twilio) com cabeçalho de mídia aceitam `header.media_file` como multipart ou signed blob ID; o serviço o armazena e gera `header.media_url` para o provedor. `Idempotency-Key` é opcional: quando omitido, cada requisição é um novo envio; quando informado, uma nova tentativa idêntica retorna a resposta original e um payload diferente retorna `409`. O HTTP `202` confirma enfileiramento local, não entrega do provedor.
- Webhooks com payload enriquecido e segredo global HMAC-SHA256.
- Em instalações hospedadas, o acesso por tokens de API e a entrega de webhooks de saída exigem a funcionalidade de conta `api_and_webhooks`; instalações autogerenciadas permanecem habilitadas por padrão.
- Evento de webhook `inbox_updated` para mudancas de estado e desconexao de inboxes.
- Dashboard Apps para extensoes embutidas via iFrame por contexto; usuarios autenticados da conta podem le-los, mas somente administradores podem cria-los, atualiza-los ou exclui-los.
- Dashboard Scripts (Super Admin) para customizacao global sem alterar core.
- Platform Apps para integracoes externas de alto nivel via API.
- Integracoes de negocio: Slack, Linear, Shopify, WooCommerce, Notion, CRM, Google Agenda e Tarefas.
- O Slack oferece `two_way` (padrao) e `alert`; este ultimo preserva a sincronizacao para o Slack, mas descarta respostas recebidas no topico para que nunca cheguem ao cliente.
- Tarefas é protegida pelo recurso de conta `activities` e por um `Integrations::Hook` de conta habilitado; o mesmo par controla visibilidade da integração, acesso à API, rota e item do sidebar.
- `/activities` persiste a visualização calendário/lista e seus critérios operacionais na query da rota. Sem `status` —ou com valor inválido— inicia em `all` e não envia filtro; valores explícitos válidos são preservados. O calendário continua sem paginação; a lista usa busca por título, ordenação e agrupamento no servidor, e metadados opcionais de `page`/`per_page`.
- Consultas do calendário usam a interseção explícita `overlaps_from`/`overlaps_to`. O cliente projeta uma tarefa de vários dias em cada data visível intersectada, não somente na data de início.
- A autorização usa três permissões de role personalizada: `task_manage` cria tarefas e gerencia somente as atribuídas ao usuário ou criadas por ele, `task_view_all` adiciona leitura global sem edição e `task_reports_view` habilita relatórios e seus detalhamentos somente leitura. Agentes padrão recebem implicitamente o escopo próprio/atribuído; administradores mantêm acesso total e exclusão exclusiva.
- `AccountTask` é a fonte de verdade para tipo, prioridade, responsável, participantes, convidados, contato/conversa e vínculos únicos com Kanban e `CalendarEvent`; persiste pendente/em andamento/concluída/cancelada e deriva vencida por `ends_at`; todos os IDs são resolvidos na conta atual.
- `ActivityType#color` armazena um dos 22 identificadores da paleta visual compartilhada com o Google Agenda. Uma migração converte as seis cores legadas e a UI reutiliza um único mapa de classes; o status adiciona decoração sem substituir o fundo do tipo.
- `outcome_summary` registra o resultado do encerramento e é obrigatório na UI e no modelo para `completed` e `cancelled`; ao reabrir, ele é preservado como histórico editável.
- `AccountTasks::TriggerDueNotificationsJob` roda a cada minuto e cria uma única notificação `account_task_due` em `ends_at`, exclusivamente para `assignee_id` e somente enquanto a tarefa estiver pendente/em andamento e Tarefas disponível. O responsável pode marcá-la como vista ou adiá-la via `snoozed_until`; o reativador global volta a publicá-la automaticamente. Reagendar, reatribuir ou encerrar remove o aviso anterior para recalculá-lo.
- Raízes recorrentes persistem tipo, intervalo, dias e limite por data ou quantidade. `AccountTasks::RecurrenceService` materializa até 100 tarefas filhas independentes, herda responsável/contexto/participantes/Kanban/Google, atualiza ocorrências abertas e preserva as encerradas.
- Referências opcionais da tarefa e da projeção `CalendarEvent` usam `ON DELETE SET NULL`. A tarefa guarda snapshots de criador, responsável, contato, conversa e item Kanban; ao excluir relações, limpa IDs ativos, resincroniza Google e mantém rótulos históricos legíveis. A cascata do contato tem um único proprietário por nível (`ContactInbox` → conversa → mensagem), evitando jobs duplicados.
- Excluir um `AccountUser` limpa de forma síncrona atribuições, participações e avisos de vencimento somente nessa conta; após o commit, resincroniza os eventos Google afetados para remover o antigo convidado. Excluir uma tarefa preserva o item Kanban gerenciado, remove seu metadado de propriedade e tenta novamente uma falha ao cancelar no Google.
- `/account_tasks` coordena transacionalmente a tarefa e um único item Kanban livre ou ligado ao cliente. A edição atualiza ou move o mesmo item; desvincular não o exclui.
- A UI carrega e mostra Kanban somente quando a conta possui `kanban_board`; a API ignora novos vínculos Kanban enquanto o recurso está desabilitado e preserva qualquer vínculo anterior oculto ao editar a tarefa.
- Ao selecionar uma conversa, o editor carrega seus itens Kanban visíveis. Vincular um item existente não o modifica e ele pode ser compartilhado por várias tarefas; “Criar novo” mantém o fluxo gerenciado por funil/etapa.
- O ReplyBox oferece criação rápida somente quando o recurso e o hook de Tarefas estão habilitados. Tipos, agentes, funis e capacidades Google são carregados sob demanda antes de abrir `TaskDialog` com contato e conversa atuais; o diálogo resolve automaticamente os itens Kanban relacionados.
- O ContactPanel mostra um acordeão específico de Tarefas com o padrão visual do calendário e consulta `/account_tasks?contact_id=...&status=open`; cada cartão mostra o `display_id` estável da conversa vinculada e o filtro inclui estados persistidos pendente/em andamento, mantendo vencimentos derivados e acompanhamento ao trocar a conversa do contato.
- `/activities` usa uma projeção `CalendarEvent` para sincronização externa opcional com início/fim exatos e participantes sem duplicação; falhas externas ficam visíveis sem reverter dados locais válidos.
- No mobile, `/activities` reorganiza filtros e navegação, mas preserva a área mensal do desktop com rolagem horizontal para não comprimir suas células. `TaskDialog` limita a área rolável com `dvh`, empilha o cabeçalho e mantém o rodapé fora do conteúdo rolável.
- `TaskDialog` abre registros existentes no modo leitura, entra explicitamente na edição e solicita `outcome_summary` em um diálogo secundário ao concluir/cancelar. A exclusão exige confirmação, aparece somente para administradores e `AccountTaskPolicy#destroy?` aplica a mesma restrição na API.
- O detalhe do item Kanban mostra a aba operacional de Tarefas somente com recurso e hook habilitados; consulta `/account_tasks?kanban_item_id=...`, mantém o histórico do item em uma aba separada e preenche contato, conversa e item ao criar.
- `AccountTasks::KanbanHistoryService` adiciona eventos `account_task_changed` ao histórico JSONB limitado do item dentro da transação local; registra o ciclo de vida e alterações de vínculo sem duplicá-los como mensagens da conversa.
- O contrato CRUD completo de Tarefas e Tipos de tarefa com escopo de conta é mantido nas fontes modulares de `swagger/`, nos documentos Swagger resolvidos e por audiência, em `docs/openapi.yml` e na coleção Postman gerada. Ele documenta filtros, `q`, interseção de intervalo, allowlists de ordenação segura, metadados de paginação opcional, relacionamentos enriquecidos, recorrência, condições de Kanban/Google, permissões e respostas de validação.
- Relatórios adiciona uma rota visível somente com recurso e hook ativos e `GET /account_tasks/reports?since=&until=`, autorizado apenas para administradores e `task_reports_view`. `AccountTasks::ReportsService` filtra por `COALESCE(ends_at, starts_at)`, gera a série diária de concluídas e agrega total, pendentes, em andamento, concluídas, vencidas e canceladas por responsável e tipo. Cada tarefa pertence a uma única categoria de status. Gráficos e linhas abrem um drawer que consulta `GET /account_tasks` pela data programada efetiva, responsável ou tipo; em seguida reutiliza `TaskDialog` no modo leitura. Métricas de tempo decorrido permanecem ocultas porque a tarefa ainda não persiste um timestamp de conclusão.
- Os controles Google só aparecem com o recurso habilitado, integração conectada, conexão ativa de saída, módulo `calendar` habilitado e agenda gravável disponível. Destino e convidados externos aparecem somente após ativar “Sincronizar”.
- Google Agenda usa APIs OAuth/config com escopo de conta, `CalendarConnection` selecionado, `CalendarEvent` interno e mapeamento de provedor em `ExternalCalendarEvent`; `settings.import_all_calendars` controla o escopo de entrada separado do `calendar_id` concreto de saida.
- A rota operacional `/app/accounts/:accountId/calendar` le `calendar_events` locais para dia, semana, mes, lista, criar, editar, cancelar, sync ao salvar e sync manual de fallback. `CalendarSync::PollConnectionsJob` roda a cada cinco minutos e importa mudancas Google com `last_polled_at` por calendario salvo em `CalendarConnection.settings`; eventos excluidos no Google removem suas projecoes locais vinculadas, e recorrencias sao expandidas entre um ano atras e cinco anos a frente.
- A navegação, a rota operacional, a ação do compositor e a seção do painel da conversa exigem o recurso da conta e `GoogleCalendarIntegration.connected?` com `CalendarConnection#calendar_id`; usuários com função personalizada também precisam de `calendar_manage`, e a configuração da integração continua exclusiva para administradores.
- A visao mensal limita cada celula a dois eventos visiveis para reservar espaco ao controle `+N mais`; o clique direito abre as acoes do evento e cada linha continua abrindo o editor. A cor fica em `metadata.color_id`; a exclusao permanente exige administrador e remove primeiro o evento vinculado do Google antes de apagar o registro local.
- As respostas de `calendar_events` incluem resumos leves de contato, conversa e item Kanban para seletores buscaveis; payloads de edicao enviam `null` para desvincular relacoes.
- O seletor de relacionamentos do calendario busca itens Kanban em toda a conta, sem herdar o funil ativo, e aceita IDs de itens (incluindo o formato `#ID`).
- As tarefas do checklist possuem configuracao propria de sincronizacao com o Google Agenda e calendario de destino; cada tarefa sincronizada e salva como um evento independente vinculado por `checklist_item_id`.
- O agente atribuido ao checklist e adicionado como convidado do Google e recebe o lembrete da plataforma; ao concluir ou excluir a tarefa, o evento e o lembrete pendente sao cancelados.
- O compositor de conversas carrega a conexao da conta e os calendarios gravaveis antes de abrir o `CalendarEventDialog` compartilhado; a acao explicita “Criar e enviar” formata o resultado `saved` com campos localizados e o envia uma unica vez por `createPendingMessageAndSend`, usando `metadata.google_meet_url` sem tentar criar o evento novamente se a mensagem falhar.
- O painel do contato filtra `calendar_events` por `conversation_display_id`, recalcula a cada 30 segundos o avanço Início–Fim para um ponto pulsante verde (<50%), amarelo (50–90%) ou vermelho (≥90%), deixa vencidos opacos, reutiliza `CalendarEventDialog` e consome atualizações de eventos salvos.
- `GoogleCalendar::EventMapperService` mapeia metadata do evento para campos Google de local, convidados, lembretes, recorrencia simples, disponibilidade, visibilidade, permissoes de convidados e Google Meet.
- O editor responsivo usa linhas com icones, seletor de fusos IANA e chips removiveis; a lateral coloca o contexto com a marca da instalação abaixo das permissoes dos convidados, com buscas flutuantes e o icone do canal em cada resultado de conversa; persiste destino e URL Meet.
- Google Agenda suporta importacao manual de entrada via `google_calendar_integration/import_events` e backfill Kanban legado via `google_calendar_integration/backfill_kanban`; triggers do Flow Builder ficam diferidos.
- Os assets do aplicativo PWA e splash são gerados dinamicamente a partir de `LOGO_THUMBNAIL`, rasterizando SVG via librsvg/libvips e com fallback para `NOTIFICATION_ICON`; alertas Push do sistema e badges usam `NOTIFICATION_ICON` (padrão `/favicon-badge-16x16.png`) com fallback recíproco, mas o badge monocromático não é anunciado como ícone instalável. O splash HTML desaparece dois frames após a primeira renderização do Vue, com transição de 180 ms e limite de segurança de 4 s. O fundo é configurável e o cache é invalidado por asset, cor e timestamp do blob; o favicon mantém a imagem do aplicativo, muda para a de notificações com a aba oculta ou sem foco e é restaurado no retorno.
- A confiabilidade da PWA exclui navegação autenticada do Cache Storage, limita assets Vite com fingerprint, faz o Rails servir `/sw.js` com cabeçalhos de revalidação obrigatória, reconcilia o estado realtime somente após a confirmação do `RoomChannel` e mantém o ciclo de opt-out/logout/troca de chave VAPID por usuário e dispositivo; a ativação aceita chaves VAPID Base64 ou binárias inicializadas pelo Rails e diferencia navegador incompatível, permissão bloqueada, configuração ausente, sessão expirada e falha de registro. Proxies reversos e CDNs devem preservar os cabeçalhos do worker.

### 3.11 Cadastro e onboarding

- Finalizacao guiada do perfil da conta pelo endpoint administrativo dedicado `/api/v1/accounts/:account_id/onboarding`.
- Persistencia do site como URL completa para consumidores posteriores como Help Center e enriquecimento de marca.
- Separacao entre atualizacoes gerais da conta e a conclusao da etapa `account_details`.
- O callback OAuth do Instagram preserva a pista assinada `return_to` para retomar o setup da caixa de entrada quando a autorizacao parte do onboarding.

### 3.12 Layouts de email com marca

- A feature flag de conta `branded_email_templates` habilita um layout de fallback por conta e uma substituição por caixa de Email.
- `EmailTemplate` separa layouts por instalação, conta e caixa; valida a sintaxe Liquid e o slot `content_for_layout`, e limita o corpo a 256 KiB (262.144 caracteres).
- O endpoint do layout da conta e a atualização de uma caixa de Email exigem administrador; os esquemas OpenAPI expõem o mesmo limite.

### 3.13 Seguranca e conformidade

- 2FA/MFA, SAML/SSO, funcoes personalizadas e logs de auditoria. SAML rejeita convites e autenticação de usuários associados a mais de uma conta, e as mudanças em massa de provedor só afetam usuários exclusivos da conta. O relatório de evidências de exclusão do Super Admin consulta apenas linhas retidas de `audits`: a destruição de Inbox usa sua associação com Account, enquanto as de Conversation e Contact usam a captura de `account_id` em `audited_changes`; ele nunca une registros vivos excluídos nem infere exclusões de Message.
- O endpoint Enterprise de logs de auditoria aceita os filtros opcionais `q`, `types[]`, `since`, `until` e `sort`; as datas são limitadas a épocas Unix seguras para o banco e o índice de associação da conta com data suporta a ordenação filtrada. Os filtros do dashboard ficam na URL e descartam respostas obsoletas.
- Os registros de sessao de usuario suportam uma etiqueta `custom_name` editavel pelo agente; a metadata de IP permanece interna e nao e exposta nos payloads de sessoes do dashboard.
- A autenticação web envia um ID persistente e validado de 128 bits por perfil do navegador como client ID do token. As abas reutilizam um único `UserSession`, a reautenticação rotaciona a mesma vaga e um logout bem-sucedido remove token e linha. Novos perfis recebem o seletor bloqueante apenas ao atingir `MAX_USER_SESSIONS`; clientes móveis mantêm IDs gerados e expulsão silenciosa.
- O estado de dashboard para conta suspensa mantem o widget de suporte visivel e expoe uma acao explicita para contatar o suporte. No Cloud, o guard de rotas e a tela suspensa permitem apenas que administradores acessem o faturamento para restaurar a conta; agentes permanecem na tela suspensa. O Super Admin valida uma categoria e um motivo de até 256 caracteres, adiciona eventos em `accounts.internal_attributes.suspensions`, preserva metadata interna não relacionada e permite corrigir o último evento sem alterar sua marca de tempo.
- `POST /super_admin/users/:id/resend_confirmation` é restrito ao Super Admin; ele reenvia as instruções padrão do Devise somente para usuários não confirmados e não enfileira e-mail para usuários confirmados. A página de detalhes oculta a ação depois que o usuário é confirmado.
- Protecao de licenca Mega em fluxos de deploy.
- Observabilidade de release para rastreabilidade por versao.

## 4. Operacao e validacao

### Paridade da API e coleção Postman

As rotas suportadas em `/api`, `/platform/api` e `/public/api` são comparadas com OpenAPI 3.1 por método e rota normalizada. A validação detecta operações ausentes, obsoletas ou duplicadas; ela não afirma cobertura de testes para cada campo de resposta. `bundle exec rake swagger:build` regenera Swagger e `swagger/postman_collection.json` em uma estrutura pronta para importação: os recursos da Application API ficam em pastas de primeiro nível herdando `api_access_token`, enquanto Mega Platform APIs e Mega Public APIs mantêm pastas e autenticação próprias. As variáveis da coleção centralizam `host`, `api_version`, `account_id`, credenciais e identificadores de rota. As mensagens multimídia incluem exemplos separados para selecionar um arquivo com `multipart/form-data` ou usar um `signed_blob_id` em JSON. `Idempotency-Key` é opcional e aparece desativado; pode ser habilitado com `{{$guid}}` ou uma chave fixa para verificar novas tentativas.

Mensagens programadas podem ser criadas no nível da conta com `contact_id` e `inbox_id`, sem exigir uma conversa, dentro de uma conversa ou por `POST /scheduled_outbound_messages` com telefone, e-mail, `contact_id` ou `source_id`: esta última opção resolve ou cria o contato/contact-inbox em transação e deixa a mensagem pendente sem criar uma conversa antecipadamente. Mensagens com falha são recuperadas por ações explícitas e autorizadas: tentar novamente deixa o registro pendente e o enfileira imediatamente; reagendar exige horário futuro, preserva conteúdo, parâmetros de template e anexos e mantém os limites de conta e conversa. Uma mensagem enviada pode ser programada novamente como uma cópia independente e não recorrente, com horário futuro e conteúdo editáveis, preservando destinatário, inbox, template e anexos.

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
