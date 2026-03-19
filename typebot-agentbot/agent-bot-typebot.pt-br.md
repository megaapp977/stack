# Typebot Agent Bot

Este documento descreve como o Mega se integra com o Typebot quando uma caixa de entrada está conectada a um **agente bot Typebot**.

## Visão geral

- Mensagens públicas recebidas em uma conversa pendente são encaminhadas ao Typebot. Uma sessão Typebot é iniciada se ainda não existir; caso contrário, o chat continua usando o id de sessão armazenado.
- Respostas do Typebot são enfileiradas como mensagens de bot na conversa. Quando o fluxo termina, o Mega devolve a conversa para a fila humana.
- Um subconjunto dos dados de contato, conversa e conta é enviado como **variáveis preenchidas** ao Typebot na primeira solicitação.

## Configuração (Agent Bot → Typebot)

Defina estes campos no agente bot:

- `api_url` (obrigatório): URL base do Typebot. Padrão `https://typebot.io`.
- `api_token` (opcional): token Bearer; necessário para Typebots privados.
- `public_name` (obrigatório): nome/slug público do Typebot.
- `trigger_type` (obrigatório): `all` (qualquer mensagem recebida) ou `keyword`.
- `trigger_operator` (gatilho por palavra-chave): um de `contains` (padrão), `equals`, `starts_with`, `ends_with`, `regex`.
- `trigger_value` (gatilho por palavra-chave): palavra-chave ou padrão regex a ser combinado.
- `finish_keyword` (opcional): conteúdo da mensagem recebida que força o repasse e o reset da sessão.
- `debounce_time` (opcional): segundos para atrasar o envio da solicitação ao Typebot (útil quando há vários envios rápidos).
- `default_delay_message` (opcional): segundos de espera entre várias respostas do Typebot quando chegam em lote.
- `expire_in_minutes` (opcional): se definido, o id de sessão é limpo após este tempo e a conversa é reaberta.
- Regras de ignorar (opcional):
  - `ignore_groups` (booleano): pula o Typebot para conversas em grupo (ex.: grupos do WhatsApp).
  - `ignored_targets` (array): identificadores por e-mail/telefone para ignorar o Typebot (comparação exata; telefones são normalizados para dígitos).

## Variáveis preenchidas enviadas ao Typebot

Enviadas apenas na primeira solicitação de uma sessão:

- Contato: `contact_name`, `contact_email`, `contact_phone`, `contact_id`, `contact_labels`, `contact_attributes`, `contact_custom_attribute_<key>`
- Conversa: `conversation_labels`, `conversation_id`, `conversation_display_id`, `conversation_attributes`, `custom_attribute_<key>`
- Conta: `account_id`
- Agentes: `agents_json` (array JSON com id, name, availability_status), `agents_formatted` (lista numerada com emoji de disponibilidade, ex: `1. 🟢 João`)
- Equipes: `teams_json` (array JSON com id e name), `teams_formatted` (lista numerada, ex: `1. Vendas`)

Os valores de `<key>` são sanitizados para snake_case em minúsculas.

## Fluxo de mensagens

- O Mega agrega as últimas mensagens públicas recebidas (texto + URLs de anexos) em um único payload de requisição. O último id de mensagem é enviado como `metadata.replyId`.
- Se um id de sessão estiver presente no estado, as requisições vão para `/api/v1/sessions/:sessionId/continueChat`; caso contrário, para `/api/v1/typebots/:publicName/startChat`.
- As respostas do Typebot são sequenciadas e entregues na conversa. `default_delay_message` controla o espaçamento entre múltiplas mensagens.
- Anexos do Typebot são mapeados para os tipos de arquivo do Mega (imagem, vídeo, áudio, arquivo, embed/documento). Vídeos retornam como links quando o download não é suportado.
- Rich text é convertido para texto no estilo Markdown (negrito/itálico/sublinhado) preservando separação de blocos.

## Ciclo de vida da sessão e repasse

- O estado da conversa é armazenado em `conversation.additional_attributes['typebot']` (id de sessão, id de resultado, marcadores de mensagens pendentes, contadores de sequência de saída).
- O repasse ocorre quando:
  - O Typebot marca o fluxo como concluído (status/palavras-chave) **e** todas as mensagens pendentes de saída forem enviadas, ou
  - A `finish_keyword` é recebida, ou
  - Regras de ignorar correspondem ao contato/número.
- Fechar ou reabrir uma conversa aciona o reset da sessão. `expire_in_minutes` também limpa o id de sessão e reabre a conversa ao expirar o temporizador.

## Dicas de solução de problemas

- Garanta que `public_name` corresponda ao slug público publicado no Typebot e que `api_token` esteja definido para bots privados.
- Para gatilhos por palavra-chave, confirme se tanto `trigger_operator` quanto `trigger_value` estão configurados.
- Se as respostas pararem no meio do fluxo, verifique `additional_attributes.typebot` na conversa em busca de um `session_id` antigo e considere usar a palavra-chave de finalização ou reabrir/fechar a conversa para resetar.

## MEGA_CMD — Interceptação local de comandos

Como um servidor Typebot externo geralmente não consegue fazer chamadas HTTP de volta para a instância do Mega (firewalls, isolamento de rede Docker, etc.), o MEGA_CMD oferece uma forma de executar ações localmente sem webhooks.

### Como funciona

1. No seu fluxo Typebot, inclua um **balão de texto** com um marcador de comando: `[MEGA_CMD:ação:valor]`
2. Quando o Mega recebe a resposta do Typebot, ele intercepta o marcador **antes** de enviar a mensagem para a conversa.
3. O comando é executado no lado do servidor (ex: atribuir um agente ou equipe).
4. O marcador é removido do texto — o usuário final nunca o vê.

### Ações suportadas

| Ação | Valor | Exemplo | Descrição |
|------|-------|---------|-----------|
| `assign_agent` | ID do agente | `[MEGA_CMD:assign_agent:5]` | Atribui o agente com id 5 à conversa |
| `assign_team` | ID da equipe | `[MEGA_CMD:assign_team:3]` | Atribui a equipe com id 3 à conversa |

### Exemplo em um fluxo Typebot

Um balão de texto no Typebot pode conter:

```text
Obrigado! Você será conectado à nossa equipe de suporte em breve.
[MEGA_CMD:assign_team:3]
```

O usuário vê apenas: *"Obrigado! Você será conectado à nossa equipe de suporte em breve."*

O comando pode ser combinado com texto regular. Múltiplos comandos na mesma mensagem também são suportados.

## Placeholders de listas — Menus numerados dinâmicos

A interpolação de variáveis do Typebot pode ser pouco confiável ao construir listas numeradas para WhatsApp (não suporta botões). O Mega fornece **placeholders de listas** no lado do servidor que são substituídos por listas numeradas geradas dinamicamente antes da mensagem ser entregue.

### Placeholders disponíveis

| Placeholder | Substituído por |
|-------------|----------------|
| `[TEAMS_LIST]` | Lista numerada de todas as equipes da conta, ordenadas por nome. Exemplo: `1. Vendas\n2. Suporte` |
| `[AGENTS_LIST]` | Lista numerada de agentes online com emoji de disponibilidade. Exemplo: `1. 🟢 João\n2. 🟢 Maria` |

### Como usar em um fluxo Typebot

Em um balão de texto, inclua o placeholder:

```text
Por favor selecione uma equipe:

[TEAMS_LIST]

0. ⬅️ Voltar ao menu
```

O Mega substitui `[TEAMS_LIST]` pela lista numerada real antes de entregar a mensagem.

### Escape de listas Markdown

Listas numeradas (ex: `1. Vendas`) normalmente seriam parseadas como listas ordenadas pelo renderizador Markdown do dashboard, o que renumera os itens (ex: convertendo `0.` em `3.`). O Mega insere um espaço de largura zero (U+200B) entre o dígito-ponto e o espaço para evitar isso, mantendo a numeração original tanto no WhatsApp quanto no dashboard.

## Acesso à API com token de bot

Para suportar as variáveis preenchidas com dados de agentes e equipes, os seguintes endpoints da API são acessíveis com tokens de bot:

- `GET /api/v1/accounts/:id/agents` — Listar agentes
- `GET /api/v1/accounts/:id/teams` — Listar equipes
- `GET /api/v1/accounts/:id/contacts` — Listar/criar/atualizar contatos
