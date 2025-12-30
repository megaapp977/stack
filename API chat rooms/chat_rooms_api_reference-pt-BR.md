# Referência da API de Salas de Chat

Esta documentação fornece exemplos de uso da API de Salas de Chat usando curl.

## Autenticação

Todas as solicitações requerem autenticação por meio de token de API. Você deve incluir o header `api_access_token` em cada solicitação.

```bash
# Configurar variáveis de ambiente
export API_TOKEN="seu_token_de_api"
export ACCOUNT_ID="1"
export BASE_URL="http://localhost:3000"
```

---

## Salas de Chat

### 1. Listar Salas de Chat

Lista todas as salas de chat da conta.

**Endpoint:** `GET /api/v1/accounts/:account_id/chat_rooms`

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Exemplo de resposta:**

```json
[
  {
    "id": 1,
    "name": "Equipe de Desenvolvimento",
    "description": "Sala para a equipe de desenvolvimento",
    "account_id": 1,
    "avatar_url": "https://example.com/avatar.png",
    "is_member": true,
    "member_count": 5,
    "last_message_at": 1640000000,
    "unread_count": 3,
    "members": [
      {
        "id": 1,
        "name": "João Silva",
        "email": "joao@example.com",
        "thumbnail": "https://example.com/avatar1.png",
        "availability_status": "online"
      }
    ],
    "created_at": 1640000000,
    "updated_at": 1640000000
  }
]
```

---

### 2. Criar Sala de Chat

Cria uma nova sala de chat.

**Endpoint:** `POST /api/v1/accounts/:account_id/chat_rooms`

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "chat_room": {
      "name": "Equipe de Marketing",
      "description": "Sala para coordenar campanhas de marketing"
    }
  }'
```

**Com avatar (arquivo):**

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms" \
  -H "api_access_token: $API_TOKEN" \
  -F "chat_room[name]=Equipe de Marketing" \
  -F "chat_room[description]=Sala para coordenar campanhas" \
  -F "chat_room[avatar]=@/caminho/para/avatar.png"
```

**Exemplo de resposta:**

```json
{
  "id": 2,
  "name": "Equipe de Marketing",
  "description": "Sala para coordenar campanhas de marketing",
  "account_id": 1,
  "avatar_url": null,
  "is_member": true,
  "member_count": 1,
  "last_message_at": 1640000000,
  "unread_count": 0,
  "members": [],
  "created_at": 1640000000,
  "updated_at": 1640000000
}
```

---

### 3. Obter Sala de Chat

Obtém os detalhes de uma sala de chat específica.

**Endpoint:** `GET /api/v1/accounts/:account_id/chat_rooms/:id`

```bash
export CHAT_ROOM_ID="1"

curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Exemplo de resposta:**

```json
{
  "id": 1,
  "name": "Equipe de Desenvolvimento",
  "description": "Sala para a equipe de desenvolvimento",
  "account_id": 1,
  "avatar_url": "https://example.com/avatar.png",
  "is_member": true,
  "member_count": 5,
  "last_message_at": 1640000000,
  "unread_count": 3,
  "members": [
    {
      "id": 1,
      "name": "João Silva",
      "email": "joao@example.com",
      "thumbnail": "https://example.com/avatar1.png",
      "availability_status": "online"
    }
  ],
  "created_at": 1640000000,
  "updated_at": 1640000000
}
```

---

### 4. Atualizar Sala de Chat

Atualiza os detalhes de uma sala de chat.

**Endpoint:** `PUT /api/v1/accounts/:account_id/chat_rooms/:id`

```bash
curl -X PUT \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "chat_room": {
      "name": "Equipe de Desenvolvimento - Atualizada",
      "description": "Nova descrição para a equipe"
    }
  }'
```

**Atualizar com avatar:**

```bash
curl -X PUT \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID" \
  -H "api_access_token: $API_TOKEN" \
  -F "chat_room[name]=Equipe de Desenvolvimento - Atualizada" \
  -F "chat_room[avatar]=@/caminho/para/novo_avatar.png"
```

**Exemplo de resposta:**

```json
{
  "id": 1,
  "name": "Equipe de Desenvolvimento - Atualizada",
  "description": "Nova descrição para a equipe",
  "account_id": 1,
  "avatar_url": "https://example.com/new_avatar.png",
  "is_member": true,
  "member_count": 5,
  "last_message_at": 1640000000,
  "unread_count": 3,
  "members": [...],
  "created_at": 1640000000,
  "updated_at": 1640000100
}
```

---

### 5. Excluir Sala de Chat

Exclui uma sala de chat.

**Endpoint:** `DELETE /api/v1/accounts/:account_id/chat_rooms/:id`

```bash
curl -X DELETE \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID" \
  -H "api_access_token: $API_TOKEN"
```

**Resposta:** Status `200 OK` sem conteúdo

---

### 6. Marcar como Lida

Marca todas as mensagens de uma sala como lidas para o usuário atual.

**Endpoint:** `POST /api/v1/accounts/:account_id/chat_rooms/:id/mark_as_read`

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/mark_as_read" \
  -H "api_access_token: $API_TOKEN"
```

**Resposta:** Status `200 OK` sem conteúdo

---

## Membros da Sala de Chat

### 7. Listar Membros

Lista todos os membros de uma sala de chat.

**Endpoint:** `GET /api/v1/accounts/:account_id/chat_rooms/:chat_room_id/members`

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/members" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Exemplo de resposta:**

```json
[
  {
    "id": 1,
    "name": "João Silva",
    "email": "joao@example.com",
    "account_id": 1,
    "role": "agent",
    "confirmed": true,
    "availability_status": "online",
    "thumbnail": "https://example.com/avatar1.png"
  },
  {
    "id": 2,
    "name": "Maria Oliveira",
    "email": "maria@example.com",
    "account_id": 1,
    "role": "agent",
    "confirmed": true,
    "availability_status": "offline",
    "thumbnail": "https://example.com/avatar2.png"
  }
]
```

---

### 8. Adicionar Membros

Adiciona um ou mais membros a uma sala de chat.

**Endpoint:** `POST /api/v1/accounts/:account_id/chat_rooms/:chat_room_id/members`

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/members" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "user_ids": [3, 4, 5]
  }'
```

**Exemplo de resposta:**

```json
[
  {
    "id": 3,
    "name": "Pedro Santos",
    "email": "pedro@example.com",
    "account_id": 1,
    "role": "agent",
    "confirmed": true,
    "availability_status": "online",
    "thumbnail": "https://example.com/avatar3.png"
  },
  {
    "id": 4,
    "name": "Ana Costa",
    "email": "ana@example.com",
    "account_id": 1,
    "role": "agent",
    "confirmed": true,
    "availability_status": "busy",
    "thumbnail": "https://example.com/avatar4.png"
  }
]
```

---

### 9. Atualizar Membros

Atualiza a lista completa de membros de uma sala (adiciona e/ou remove membros).

**Endpoint:** `PATCH /api/v1/accounts/:account_id/chat_rooms/:chat_room_id/members`

```bash
curl -X PATCH \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/members" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "user_ids": [1, 2, 3, 6]
  }'
```

> **Nota:** Esta operação estabelece a lista completa de membros. Os usuários não incluídos em `user_ids` serão removidos, e os novos serão adicionados.

**Exemplo de resposta:**

```json
[
  {
    "id": 1,
    "name": "João Silva",
    "email": "joao@example.com",
    "account_id": 1,
    "role": "agent",
    "confirmed": true,
    "availability_status": "online",
    "thumbnail": "https://example.com/avatar1.png"
  },
  {
    "id": 2,
    "name": "Maria Oliveira",
    "email": "maria@example.com",
    "account_id": 1,
    "role": "agent",
    "confirmed": true,
    "availability_status": "offline",
    "thumbnail": "https://example.com/avatar2.png"
  },
  {
    "id": 3,
    "name": "Pedro Santos",
    "email": "pedro@example.com",
    "account_id": 1,
    "role": "agent",
    "confirmed": true,
    "availability_status": "online",
    "thumbnail": "https://example.com/avatar3.png"
  },
  {
    "id": 6,
    "name": "Carlos Almeida",
    "email": "carlos@example.com",
    "account_id": 1,
    "role": "agent",
    "confirmed": true,
    "availability_status": "busy",
    "thumbnail": "https://example.com/avatar6.png"
  }
]
```

---

### 10. Remover Membros

Remove um ou mais membros de uma sala de chat.

**Endpoint:** `DELETE /api/v1/accounts/:account_id/chat_rooms/:chat_room_id/members`

```bash
curl -X DELETE \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/members" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "user_ids": [4, 5]
  }'
```

**Resposta:** Status `200 OK` sem conteúdo

---

## Mensagens da Sala de Chat

### 11. Listar Mensagens

Lista as mensagens de uma sala de chat com paginação.

**Endpoint:** `GET /api/v1/accounts/:account_id/chat_rooms/:chat_room_id/messages`

```bash
# Listar mensagens (página 1)
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Com paginação:**

```bash
# Página 2, 50 mensagens por página
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/messages?page=2&per_page=50" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Headers de resposta com informações de paginação:**

```
X-Total-Count: 150
X-Current-Page: 1
X-Per-Page: 20
X-Total-Pages: 8
```

**Exemplo de resposta:**

```json
[
  {
    "id": 1,
    "content": "Olá equipe, como está o andamento do projeto?",
    "message_type": "outgoing",
    "content_type": "text",
    "content_attributes": {},
    "created_at": 1640000000,
    "conversation_id": 1,
    "room_name": "Equipe de Desenvolvimento",
    "sender": {
      "id": 1,
      "name": "João Silva",
      "email": "joao@example.com",
      "thumbnail": "https://example.com/avatar1.png",
      "availability_status": "online"
    },
    "attachments": [],
    "status": "sent"
  },
  {
    "id": 2,
    "content": "Tudo bem, estamos avançando conforme o planejado",
    "message_type": "incoming",
    "content_type": "text",
    "content_attributes": {
      "in_reply_to": 1
    },
    "created_at": 1640000060,
    "conversation_id": 1,
    "room_name": "Equipe de Desenvolvimento",
    "sender": {
      "id": 2,
      "name": "Maria Oliveira",
      "email": "maria@example.com",
      "thumbnail": "https://example.com/avatar2.png",
      "availability_status": "online"
    },
    "attachments": [],
    "status": "read",
    "in_reply_to": {
      "id": 1,
      "content": "Olá equipe, como está o andamento do projeto?",
      "sender": {
        "id": 1,
        "name": "João Silva"
      }
    }
  }
]
```

---

### 12. Enviar Mensagem

Envia uma nova mensagem para uma sala de chat.

**Endpoint:** `POST /api/v1/accounts/:account_id/chat_rooms/:chat_room_id/messages`

**Mensagem de texto simples:**

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "chat_room_message": {
      "content": "Esta é uma mensagem de teste",
      "message_type": "outgoing"
    }
  }'
```

**Mensagem com echo_id (para sincronização):**

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "chat_room_message": {
      "content": "Mensagem com identificador temporário",
      "message_type": "outgoing",
      "echo_id": "temp-msg-12345"
    }
  }'
```

**Mensagem em resposta a outra mensagem:**

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "chat_room_message": {
      "content": "Respondendo à mensagem anterior",
      "message_type": "outgoing",
      "content_attributes": {
        "in_reply_to": 123
      }
    }
  }'
```

**Mensagem com arquivos anexos:**

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/messages" \
  -H "api_access_token: $API_TOKEN" \
  -F "chat_room_message[content]=Anexo alguns arquivos" \
  -F "chat_room_message[message_type]=outgoing" \
  -F "chat_room_message[attachments][]=@/caminho/para/documento.pdf" \
  -F "chat_room_message[attachments][]=@/caminho/para/imagem.png"
```

**Exemplo de resposta:**

```json
{
  "id": 150,
  "content": "Esta é uma mensagem de teste",
  "message_type": "outgoing",
  "content_type": "text",
  "content_attributes": {},
  "created_at": 1640000500,
  "conversation_id": 1,
  "room_name": "Equipe de Desenvolvimento",
  "sender": {
    "id": 1,
    "name": "João Silva",
    "email": "joao@example.com",
    "thumbnail": "https://example.com/avatar1.png",
    "availability_status": "online"
  },
  "attachments": [],
  "status": "sent"
}
```

---

## Códigos de Error

### Erros comuns

- **401 Unauthorized**: Token de API inválido ou ausente
- **403 Forbidden**:
  - O recurso de salas de chat não está habilitado para a conta
  - O usuário não é membro da sala de chat
  - Permissões insuficientes
- **404 Not Found**: Recurso não encontrado (sala, mensagem, usuário)
- **422 Unprocessable Entity**: Erros de validação

**Exemplo de erro:**

```json
{
  "error": "Feature chat_rooms is not enabled for this account"
}
```

```json
{
  "message": "Name can't be blank"
}
```

---

## Notas Adicionais

### Paginação em Mensagens

- Padrão: 20 mensagens por página
- Máximo: 50 mensagens por página
- As mensagens são retornadas da mais recente para a mais antiga
- Use os headers de resposta para informações de paginação

### Estados da Mensagem

- `sent`: Mensagem enviada
- `delivered`: Mensagem entregue (todos os membros receberam notificação)
- `read`: Mensagem lida por todos os membros (exceto o remetente)

### Anexos

- Suporta múltiplos arquivos por mensagem
- Use `multipart/form-data` para enviar arquivos
- Os arquivos podem ser imagens, documentos, vídeos, etc.

### Respostas a Mensagens

- Use `content_attributes.in_reply_to` com o ID da mensagem original
- A API retorna os dados da mensagem original no campo `in_reply_to`

### Permissões

- Apenas membros de uma sala podem visualizar e enviar mensagens
- Apenas administradores podem visualizar todas as salas (listar)
- Usuários normais apenas veem as salas das quais são membros
- Apenas administradores podem criar/atualizar/excluir salas
