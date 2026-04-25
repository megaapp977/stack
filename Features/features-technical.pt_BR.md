# MEGA - Detalhe Tecnico de Funcionalidades (PT-BR)

Versao: Enterprise
Ultima atualizacao: 25 de abril de 2026
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
- WhatsApp Evolution, WAHA e Uazapi: provedores alternativos com suporte multimidia e grupos.
- Notificame: variante oficial orientada a operacao LATAM.
- Instagram, Facebook, TikTok, Telegram, X, SMS e Email como inboxes.
- API Channel: gateway generico para plataformas proprietarias via API/webhooks.
- Voz Twilio e chamadas WhatsApp Cloud: fluxo WebRTC com timeline unificada.

### 3.2 Nucleo de conversas

- Modelo de status: open, pending, resolved, snoozed.
- Modelo de prioridade: tratamento de urgencia por conversa.
- Participantes: colaboracao multiagente na mesma thread.
- Rascunhos e fixadas: continuidade de trabalho por agente.
- Filtros avancados e visoes personalizadas: segmentacao para alto volume.
- Assignment V2: distribuicao inteligente com capacidade e regras.

### 3.3 Automacao e bots

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

- Agent Bots por inbox com handover inteligente.
- Typebot estendido com comandos MEGA_CMD para atribuicao de agente/equipe.
- Assinaturas de webhook por canal para validar autenticidade de eventos de saida.

### 3.4 IA Captain

- Provedores suportados: OpenAI, Anthropic, Google, Azure OpenAI, Bedrock, DeepSeek.
- Assistants: configuracao por inbox com instrucoes e contexto.
- Captain Documents: upload, indexacao e campos de auto-sincronizacao.
- Captain Scenarios: regras de ativacao e prioridade.
- Captain Custom Tools: integracoes HTTP com GET, POST, PUT, PATCH e DELETE.
- MCP Servers: extensao de capacidades via Model Context Protocol.
- Auto-resolve mode: evaluated, legacy ou disabled por conta.

### 3.5 CRM e gestao de contatos

- Atributos personalizados por tipo de dado e uso em automacoes.
- Visibilidade por papel para atributos sensiveis (Enterprise).
- Etiquetas em contatos e conversas.
- Empresas agrupadas por dominio com timeline unificada.
- Bloqueio ativo no WhatsApp para descartar mensagens recebidas de contatos bloqueados.

### 3.6 Campanhas

- Ongoing campaigns para widget/live chat.
- One-off campaigns para WhatsApp, SMS e API Channel.
- Construtor de templates Meta com ciclo de aprovacao e sincronizacao.
- Controle de velocidade, rotacao multi-inbox e metricas de execucao.

### 3.7 Help Center

- Artigos multi-idioma com estado por idioma.
- Editor com menu slash e suporte nativo a tabelas.
- Insercao de artigos em conversa com busca estavel em popover.
- Embedding search no Enterprise para busca semantica.

### 3.8 Kanban comercial (Mega)

- Funis com etapas configuraveis e etapa padrao.
- Visoes board e list para fluxos distintos de equipe.
- Filtros por inbox, canal, etapa e atividade.
- Workspace 360 do item: checklist, notas, anexos, ofertas, agentes e atributos.
- Relacao nativa com contato e conversa.
- Automacoes por etapa e mensagens rapidas.
- Sincronizacao em tempo real com lista de chats e painel de contato.

### 3.9 Integracoes e extensibilidade

- Webhooks com payload enriquecido e segredo global HMAC-SHA256.
- Dashboard Apps para extensoes embutidas via iFrame por contexto.
- Dashboard Scripts (Super Admin) para customizacao global sem alterar core.
- Platform Apps para integracoes externas de alto nivel via API.
- Integracoes de negocio: Slack, Linear, Shopify, WooCommerce, Notion e CRM.

### 3.10 Seguranca e conformidade

- 2FA/MFA, SAML/SSO, funcoes personalizadas e logs de auditoria.
- Protecao de licenca Mega em fluxos de deploy.
- Observabilidade de release para rastreabilidade por versao.

## 4. Operacao e validacao

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
