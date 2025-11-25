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
