# Referência da API de Mensagens Agendadas

Esta documentação fornece exemplos de uso da API de Mensagens Agendadas usando curl.

## Autenticação

Todas as requisições requerem autenticação por token de API. Você deve incluir o header `api_access_token` em cada requisição.

```bash
# Configurar variáveis de ambiente
export API_TOKEN="seu_token_de_api"
export ACCOUNT_ID="1"
export BASE_URL="http://localhost:3000"
```

---

## Mensagens Agendadas (Nível de Conta)

### 1. Listar Mensagens Agendadas

Lista todas as mensagens agendadas da conta, ordenadas por data de agendamento decrescente.

**Endpoint:** `GET /api/v1/accounts/:account_id/scheduled_messages`

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Resposta de exemplo:**

```json
{
  "payload": [
    {
      "id": 1,
      "content": "Lembrete: Reunião amanhã às 10h",
      "scheduled_at": 1738836000,
      "sent_at": null,
      "title": "Lembrete de reunião",
      "inbox_id": 5,
      "inbox_name": "WhatsApp Business",
      "conversation_id": 123,
      "contact_id": 456,
      "contact_name": "João Silva",
      "contact_phone": "+5511987654321",
      "contact_email": "joao@exemplo.com",
      "message_id": null,
      "created_at": 1738749600,
      "status": "pending",
      "error_message": null,
      "template_params": null,
      "attachments": [],
      "recurrence_type": "none",
      "recurrence_interval": null,
      "recurrence_days": null,
      "recurrence_end_type": null,
      "recurrence_end_date": null,
      "recurrence_max_occurrences": null,
      "recurrence_count": 0,
      "parent_id": null,
      "assignee_id": 10,
      "assignee_name": "Maria Santos",
      "assignee_avatar_url": "https://exemplo.com/avatar.png"
    }
  ]
}
```

**Status possíveis:**

- `pending`: Mensagem aguardando envio
- `sent`: Mensagem enviada com sucesso
- `failed`: Falha no envio

---

### 2. Visualizar Mensagem Agendada

Obtém os detalhes de uma mensagem agendada específica.

**Endpoint:** `GET /api/v1/accounts/:account_id/scheduled_messages/:id`

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages/1" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Resposta:** Mesma estrutura de um item da listagem.

---

### 3. Criar Mensagem Agendada

Cria uma nova mensagem agendada no nível da conta.

**Endpoint:** `POST /api/v1/accounts/:account_id/scheduled_messages`

#### 3.1 Mensagem Simples

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Olá, esta é uma mensagem agendada",
    "scheduled_at": "2026-02-06T15:00:00Z",
    "title": "Acompanhamento do cliente"
  }'
```

#### 3.2 Mensagem com Anexos

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -F "inbox_id=5" \
  -F "contact_id=456" \
  -F "content=Segue em anexo o documento solicitado" \
  -F "scheduled_at=2026-02-06T15:00:00Z" \
  -F "title=Envio de documento" \
  -F "attachments[]=@/caminho/para/documento.pdf" \
  -F "attachments[]=@/caminho/para/imagem.jpg"
```

**Limite:** Máximo de 15 anexos por mensagem.

#### 3.3 Mensagem com Template do WhatsApp

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Template de confirmação",
    "scheduled_at": "2026-02-06T15:00:00Z",
    "title": "Confirmar consulta",
    "template_params": {
      "name": "appointment_reminder",
      "category": "UTILITY",
      "language": "pt_BR",
      "namespace": "seu_namespace",
      "processed_params": {
        "header": {},
        "body": [
          {"type": "text", "text": "João Silva"},
          {"type": "text", "text": "10:00"},
          {"type": "text", "text": "6 de fevereiro"}
        ],
        "buttons": []
      }
    }
  }'
```

#### 3.4 Mensagem Recorrente

```bash
# Mensagem diária repetindo 10 vezes
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Lembrete diário",
    "scheduled_at": "2026-02-06T09:00:00Z",
    "title": "Lembrete matinal",
    "recurrence_type": "daily",
    "recurrence_interval": 1,
    "recurrence_end_type": "after_occurrences",
    "recurrence_max_occurrences": 10
  }'
```

```bash
# Mensagem semanal repetindo até uma data
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Relatório semanal",
    "scheduled_at": "2026-02-10T10:00:00Z",
    "title": "Relatório executivo",
    "recurrence_type": "weekly",
    "recurrence_interval": 1,
    "recurrence_days": [1],
    "recurrence_end_type": "on_date",
    "recurrence_end_date": "2026-12-31"
  }'
```

```bash
# Mensagem mensal infinita
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Lembrete mensal",
    "scheduled_at": "2026-03-01T12:00:00Z",
    "title": "Acompanhamento mensal",
    "recurrence_type": "monthly",
    "recurrence_interval": 1,
    "recurrence_end_type": "never"
  }'
```

**Parâmetros de recorrência:**

- `recurrence_type`: `none` (padrão), `daily`, `weekly`, `monthly`, `yearly`
- `recurrence_interval`: Intervalo de repetição (ex: 2 = a cada 2 dias/semanas/meses)
- `recurrence_days`: Array de dias da semana (0=Domingo, 6=Sábado) - Apenas para `weekly`
- `recurrence_end_type`: `never`, `on_date`, `after_occurrences`
- `recurrence_end_date`: Data até a qual repetir (ISO 8601) - Obrigatório se `recurrence_end_type` for `on_date`
- `recurrence_max_occurrences`: Número máximo de ocorrências - Obrigatório se `recurrence_end_type` for `after_occurrences`

**Resposta de exemplo:**

```json
{
  "id": 2,
  "content": "Olá, esta é uma mensagem agendada",
  "scheduled_at": 1738854000,
  "sent_at": null,
  "title": "Acompanhamento do cliente",
  "inbox_id": 5,
  "inbox_name": "WhatsApp Business",
  "conversation_id": null,
  "contact_id": 456,
  "contact_name": "João Silva",
  "message_id": null,
  "created_at": 1738767600,
  "status": "pending",
  "error_message": null,
  "template_params": null,
  "attachments": [],
  "recurrence_type": "none"
}
```

---

### 4. Atualizar Mensagem Agendada

Atualiza uma mensagem agendada existente. Somente mensagens com status `pending` podem ser atualizadas.

**Endpoint:** `PUT /api/v1/accounts/:account_id/scheduled_messages/:id`

```bash
curl -X PUT \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages/1" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "content": "Mensagem atualizada",
    "scheduled_at": "2026-02-07T16:00:00Z",
    "title": "Título atualizado"
  }'
```

**Nota:** O campo `status` não pode ser modificado manualmente. É atualizado automaticamente quando a mensagem é enviada ou falha.

---

### 5. Excluir Mensagem Agendada

Exclui uma mensagem agendada. Pode ser excluída em qualquer status.

**Endpoint:** `DELETE /api/v1/accounts/:account_id/scheduled_messages/:id`

```bash
curl -X DELETE \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages/1" \
  -H "api_access_token: $API_TOKEN"
```

**Resposta:** `204 No Content`

---

## Mensagens Agendadas por Conversa

### 1. Listar Mensagens de uma Conversa

Lista todas as mensagens agendadas associadas a um contato específico (inclui todas as suas conversas).

**Endpoint:** `GET /api/v1/accounts/:account_id/conversations/:conversation_id/scheduled_messages`

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Resposta de exemplo:**

```json
{
  "payload": [
    {
      "id": 1,
      "content": "Acompanhamento programado",
      "scheduled_at": 1738836000,
      "sent_at": null,
      "title": "Acompanhamento",
      "inbox_id": 5,
      "conversation_id": 123,
      "message_id": null,
      "created_at": 1738749600,
      "status": "pending",
      "error_message": null,
      "template_params": null,
      "attachments": []
    }
  ]
}
```

---

### 2. Visualizar Mensagem Agendada

Obtém os detalhes de uma mensagem agendada específica.

**Endpoint:** `GET /api/v1/accounts/:account_id/conversations/:conversation_id/scheduled_messages/:id`

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages/1" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

---

### 3. Criar Mensagem Agendada na Conversa

Cria uma mensagem agendada dentro de uma conversa existente.

**Endpoint:** `POST /api/v1/accounts/:account_id/conversations/:conversation_id/scheduled_messages`

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "scheduled_message": {
      "content": "Esta é uma mensagem agendada da conversa",
      "scheduled_at": "2026-02-06T15:00:00Z",
      "title": "Acompanhamento automático",
      "inbox_id": 5
    }
  }'
```

**Com anexos:**

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -F "scheduled_message[content]=Mensagem com arquivo" \
  -F "scheduled_message[scheduled_at]=2026-02-06T15:00:00Z" \
  -F "scheduled_message[title]=Envio de documento" \
  -F "scheduled_message[inbox_id]=5" \
  -F "scheduled_message[attachments][]=@/caminho/para/arquivo.pdf"
```

---

### 4. Atualizar Mensagem Agendada

Atualiza uma mensagem agendada em uma conversa.

**Endpoint:** `PUT /api/v1/accounts/:account_id/conversations/:conversation_id/scheduled_messages/:id`

```bash
curl -X PUT \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages/1" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "scheduled_message": {
      "content": "Mensagem atualizada da conversa",
      "scheduled_at": "2026-02-07T16:00:00Z"
    }
  }'
```

---

### 5. Excluir Mensagem Agendada

Exclui uma mensagem agendada de uma conversa.

**Endpoint:** `DELETE /api/v1/accounts/:account_id/conversations/:conversation_id/scheduled_messages/:id`

```bash
curl -X DELETE \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages/1" \
  -H "api_access_token: $API_TOKEN"
```

**Resposta:** `200 OK`

---

### 6. Contar Mensagens Agendadas

Conta as mensagens agendadas de uma conversa, com opção de filtrar por status.

**Endpoint:** `GET /api/v1/accounts/:account_id/conversations/:conversation_id/scheduled_messages/count`

```bash
# Contar todas as mensagens
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages/count" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"

# Contar mensagens pendentes
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages/count?status=pending" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Resposta:**

```json
{
  "count": 5
}
```

---

## Casos de Uso Comuns

### 1. Acompanhamento Automático Pós-Venda

```bash
# Agendar mensagem de acompanhamento 24 horas depois
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Olá, como foi sua experiência com nosso produto?",
    "scheduled_at": "2026-02-07T10:00:00Z",
    "title": "Acompanhamento pós-venda"
  }'
```

### 2. Lembretes de Consultas

```bash
# Lembrete 1 dia antes
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Lembrete: Você tem uma consulta amanhã às 15h",
    "scheduled_at": "2026-02-09T09:00:00Z",
    "title": "Lembrete de consulta"
  }'
```

### 3. Newsletters Semanais

```bash
# Newsletter toda segunda-feira às 9h
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Bom dia! Aqui está sua newsletter semanal",
    "scheduled_at": "2026-02-10T09:00:00Z",
    "title": "Newsletter Semanal",
    "recurrence_type": "weekly",
    "recurrence_interval": 1,
    "recurrence_days": [1],
    "recurrence_end_type": "never"
  }'
```

### 4. Campanha de Nutrição de Leads

```bash
# Mensagem 1: Imediata
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 789,
    "content": "Obrigado pelo seu interesse! Aqui está mais informação...",
    "scheduled_at": "2026-02-06T10:00:00Z",
    "title": "Campanha - Dia 0"
  }'

# Mensagem 2: 3 dias depois
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 789,
    "content": "Você teve oportunidade de revisar as informações?",
    "scheduled_at": "2026-02-09T10:00:00Z",
    "title": "Campanha - Dia 3"
  }'

# Mensagem 3: 7 dias depois
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 789,
    "content": "Oferta especial disponível por tempo limitado",
    "scheduled_at": "2026-02-13T10:00:00Z",
    "title": "Campanha - Dia 7"
  }'
```

---

## Permissões

### Edição Padrão (OSS)

As permissões são controladas pela política `ScheduledMessagePolicy`:

- **Administradores**: Acesso completo
- **Agentes**: Podem gerenciar suas próprias mensagens agendadas
- **Supervisor de inbox**: Pode gerenciar mensagens do inbox supervisionado

### Enterprise Edition

Na edição Enterprise, pode-se atribuir a permissão granular:

- `scheduled_message_manage`: Permite gerenciar todas as mensagens agendadas da conta

Esta permissão pode ser atribuída a Funções Personalizadas (Custom Roles).

---

## Notas Importantes

1. **Fuso Horário**: Todas as datas devem ser enviadas no formato ISO 8601 (UTC). O sistema as converterá conforme o fuso horário da conta.

2. **Validação de Data**: Não é possível agendar uma mensagem no passado.

3. **Limite de Anexos**: Máximo de 15 arquivos por mensagem.

4. **Status**:
   - As mensagens são criadas com status `pending`
   - Mudam para `sent` quando enviadas com sucesso
   - Mudam para `failed` se houver erro no envio

5. **Job Assíncrono**: As mensagens são enviadas através do `ScheduledMessageJob` que executa na data/hora programada.

6. **Recorrência**:
   - Mensagens recorrentes criam automaticamente a próxima ocorrência após serem enviadas
   - A recorrência pode ser interrompida excluindo a mensagem pai
   - O campo `parent_id` indica se é uma ocorrência de uma mensagem recorrente

7. **Templates do WhatsApp**:
   - Os templates devem estar previamente aprovados na API do WhatsApp Business
   - Os parâmetros devem coincidir exatamente com a estrutura do template

8. **Exclusão**:
   - Excluir uma mensagem `pending` cancela seu envio
   - Excluir uma mensagem recorrente pai interrompe todas as ocorrências futuras

---

## Códigos de Erro Comuns

- `404 Not Found`: A mensagem agendada não existe ou não pertence à conta
- `422 Unprocessable Entity`: Erros de validação (data inválida, campos obrigatórios, etc.)
- `403 Forbidden`: Sem permissões para realizar a ação

**Exemplos de erros:**

```json
{
  "error": "Scheduled at can't be in the past"
}
```

```json
{
  "error": "Content can't be blank"
}
```

```json
{
  "error": "Must provide either contact_id or conversation_id"
}
```

---

## Eventos de Webhook

O sistema emite os seguintes eventos para mensagens agendadas:

- `scheduled_message.created`: Quando uma mensagem agendada é criada
- `scheduled_message.updated`: Quando uma mensagem agendada é atualizada
- `scheduled_message.deleted`: Quando uma mensagem agendada é excluída

Estes eventos podem ser capturados através de webhooks configurados na conta.

---

