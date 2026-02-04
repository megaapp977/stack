# Chat Rooms API Reference

Esta documentación proporciona ejemplos de uso de la API de Chat Rooms usando curl.

## Autenticación

Todas las peticiones requieren autenticación mediante token de API. Debes incluir el header `api_access_token` en cada petición.

```bash
# Configurar variables de entorno
export API_TOKEN="tu_token_de_api"
export ACCOUNT_ID="1"
export BASE_URL="http://localhost:3000"
```

---

## Chat Rooms

### 1. Listar Chat Rooms

Lista todas las salas de chat de la cuenta.

**Endpoint:** `GET /api/v1/accounts/:account_id/chat_rooms`

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Respuesta de ejemplo:**
```json
[
  {
    "id": 1,
    "name": "Equipo de Desarrollo",
    "description": "Sala para el equipo de desarrollo",
    "account_id": 1,
    "avatar_url": "https://example.com/avatar.png",
    "is_member": true,
    "member_count": 5,
    "last_message_at": 1640000000,
    "unread_count": 3,
    "members": [
      {
        "id": 1,
        "name": "Juan Pérez",
        "email": "juan@example.com",
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

### 2. Crear Chat Room

Crea una nueva sala de chat.

**Endpoint:** `POST /api/v1/accounts/:account_id/chat_rooms`

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "chat_room": {
      "name": "Equipo de Marketing",
      "description": "Sala para coordinar campañas de marketing"
    }
  }'
```

**Con avatar (archivo):**
```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms" \
  -H "api_access_token: $API_TOKEN" \
  -F "chat_room[name]=Equipo de Marketing" \
  -F "chat_room[description]=Sala para coordinar campañas" \
  -F "chat_room[avatar]=@/ruta/al/avatar.png"
```

**Respuesta de ejemplo:**
```json
{
  "id": 2,
  "name": "Equipo de Marketing",
  "description": "Sala para coordinar campañas de marketing",
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

### 3. Obtener Chat Room

Obtiene los detalles de una sala de chat específica.

**Endpoint:** `GET /api/v1/accounts/:account_id/chat_rooms/:id`

```bash
export CHAT_ROOM_ID="1"

curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Respuesta de ejemplo:**
```json
{
  "id": 1,
  "name": "Equipo de Desarrollo",
  "description": "Sala para el equipo de desarrollo",
  "account_id": 1,
  "avatar_url": "https://example.com/avatar.png",
  "is_member": true,
  "member_count": 5,
  "last_message_at": 1640000000,
  "unread_count": 3,
  "members": [
    {
      "id": 1,
      "name": "Juan Pérez",
      "email": "juan@example.com",
      "thumbnail": "https://example.com/avatar1.png",
      "availability_status": "online"
    }
  ],
  "created_at": 1640000000,
  "updated_at": 1640000000
}
```

---

### 4. Actualizar Chat Room

Actualiza los detalles de una sala de chat.

**Endpoint:** `PUT /api/v1/accounts/:account_id/chat_rooms/:id`

```bash
curl -X PUT \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "chat_room": {
      "name": "Equipo de Desarrollo - Actualizado",
      "description": "Nueva descripción para el equipo"
    }
  }'
```

**Actualizar con avatar:**
```bash
curl -X PUT \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID" \
  -H "api_access_token: $API_TOKEN" \
  -F "chat_room[name]=Equipo de Desarrollo - Actualizado" \
  -F "chat_room[avatar]=@/ruta/al/nuevo_avatar.png"
```

**Respuesta de ejemplo:**
```json
{
  "id": 1,
  "name": "Equipo de Desarrollo - Actualizado",
  "description": "Nueva descripción para el equipo",
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

### 5. Eliminar Chat Room

Elimina una sala de chat.

**Endpoint:** `DELETE /api/v1/accounts/:account_id/chat_rooms/:id`

```bash
curl -X DELETE \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID" \
  -H "api_access_token: $API_TOKEN"
```

**Respuesta:** Status `200 OK` sin contenido

---

### 6. Marcar como Leído

Marca todos los mensajes de una sala como leídos para el usuario actual.

**Endpoint:** `POST /api/v1/accounts/:account_id/chat_rooms/:id/mark_as_read`

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/mark_as_read" \
  -H "api_access_token: $API_TOKEN"
```

**Respuesta:** Status `200 OK` sin contenido

---

## Miembros de Chat Room

### 7. Listar Miembros

Lista todos los miembros de una sala de chat.

**Endpoint:** `GET /api/v1/accounts/:account_id/chat_rooms/:chat_room_id/members`

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/members" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Respuesta de ejemplo:**
```json
[
  {
    "id": 1,
    "name": "Juan Pérez",
    "email": "juan@example.com",
    "account_id": 1,
    "role": "agent",
    "confirmed": true,
    "availability_status": "online",
    "thumbnail": "https://example.com/avatar1.png"
  },
  {
    "id": 2,
    "name": "María García",
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

### 8. Agregar Miembros

Agrega uno o más miembros a una sala de chat.

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

**Respuesta de ejemplo:**
```json
[
  {
    "id": 3,
    "name": "Pedro López",
    "email": "pedro@example.com",
    "account_id": 1,
    "role": "agent",
    "confirmed": true,
    "availability_status": "online",
    "thumbnail": "https://example.com/avatar3.png"
  },
  {
    "id": 4,
    "name": "Ana Martínez",
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

### 9. Actualizar Miembros

Actualiza la lista completa de miembros de una sala (agrega y/o elimina miembros).

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

> **Nota:** Esta operación establece la lista completa de miembros. Los usuarios no incluidos en `user_ids` serán removidos, y los nuevos serán agregados.

**Respuesta de ejemplo:**
```json
[
  {
    "id": 1,
    "name": "Juan Pérez",
    "email": "juan@example.com",
    "account_id": 1,
    "role": "agent",
    "confirmed": true,
    "availability_status": "online",
    "thumbnail": "https://example.com/avatar1.png"
  },
  {
    "id": 2,
    "name": "María García",
    "email": "maria@example.com",
    "account_id": 1,
    "role": "agent",
    "confirmed": true,
    "availability_status": "offline",
    "thumbnail": "https://example.com/avatar2.png"
  },
  {
    "id": 3,
    "name": "Pedro López",
    "email": "pedro@example.com",
    "account_id": 1,
    "role": "agent",
    "confirmed": true,
    "availability_status": "online",
    "thumbnail": "https://example.com/avatar3.png"
  },
  {
    "id": 6,
    "name": "Carlos Ruiz",
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

### 10. Eliminar Miembros

Elimina uno o más miembros de una sala de chat.

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

**Respuesta:** Status `200 OK` sin contenido

---

## Mensajes de Chat Room

### 11. Listar Mensajes

Lista los mensajes de una sala de chat con paginación.

**Endpoint:** `GET /api/v1/accounts/:account_id/chat_rooms/:chat_room_id/messages`

```bash
# Listar mensajes (página 1)
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Con paginación:**
```bash
# Página 2, 50 mensajes por página
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/messages?page=2&per_page=50" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Headers de respuesta con información de paginación:**
```
X-Total-Count: 150
X-Current-Page: 1
X-Per-Page: 20
X-Total-Pages: 8
```

**Respuesta de ejemplo:**
```json
[
  {
    "id": 1,
    "content": "Hola equipo, ¿cómo van con el proyecto?",
    "message_type": "outgoing",
    "content_type": "text",
    "content_attributes": {},
    "created_at": 1640000000,
    "conversation_id": 1,
    "room_name": "Equipo de Desarrollo",
    "sender": {
      "id": 1,
      "name": "Juan Pérez",
      "email": "juan@example.com",
      "thumbnail": "https://example.com/avatar1.png",
      "availability_status": "online"
    },
    "attachments": [],
    "status": "sent"
  },
  {
    "id": 2,
    "content": "Todo bien, estamos avanzando según lo planeado",
    "message_type": "incoming",
    "content_type": "text",
    "content_attributes": {
      "in_reply_to": 1
    },
    "created_at": 1640000060,
    "conversation_id": 1,
    "room_name": "Equipo de Desarrollo",
    "sender": {
      "id": 2,
      "name": "María García",
      "email": "maria@example.com",
      "thumbnail": "https://example.com/avatar2.png",
      "availability_status": "online"
    },
    "attachments": [],
    "status": "read",
    "in_reply_to": {
      "id": 1,
      "content": "Hola equipo, ¿cómo van con el proyecto?",
      "sender": {
        "id": 1,
        "name": "Juan Pérez"
      }
    }
  }
]
```

---

### 12. Enviar Mensaje

Envía un nuevo mensaje a una sala de chat.

**Endpoint:** `POST /api/v1/accounts/:account_id/chat_rooms/:chat_room_id/messages`

**Mensaje de texto simple:**
```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "chat_room_message": {
      "content": "Este es un mensaje de prueba",
      "message_type": "outgoing"
    }
  }'
```

**Mensaje con echo_id (para sincronización):**
```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "chat_room_message": {
      "content": "Mensaje con identificador temporal",
      "message_type": "outgoing",
      "echo_id": "temp-msg-12345"
    }
  }'
```

**Mensaje en respuesta a otro mensaje:**
```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "chat_room_message": {
      "content": "Respondiendo al mensaje anterior",
      "message_type": "outgoing",
      "content_attributes": {
        "in_reply_to": 123
      }
    }
  }'
```

**Mensaje con archivos adjuntos:**
```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/messages" \
  -H "api_access_token: $API_TOKEN" \
  -F "chat_room_message[content]=Adjunto algunos archivos" \
  -F "chat_room_message[message_type]=outgoing" \
  -F "chat_room_message[attachments][]=@/ruta/al/documento.pdf" \
  -F "chat_room_message[attachments][]=@/ruta/a/imagen.png"
```

**Respuesta de ejemplo:**
```json
{
  "id": 150,
  "content": "Este es un mensaje de prueba",
  "message_type": "outgoing",
  "content_type": "text",
  "content_attributes": {},
  "created_at": 1640000500,
  "conversation_id": 1,
  "room_name": "Equipo de Desarrollo",
  "sender": {
    "id": 1,
    "name": "Juan Pérez",
    "email": "juan@example.com",
    "thumbnail": "https://example.com/avatar1.png",
    "availability_status": "online"
  },
  "attachments": [],
  "status": "sent"
}
```

---

## Códigos de Error

### Errores comunes:

- **401 Unauthorized**: Token de API inválido o faltante
- **403 Forbidden**: 
  - La característica de chat rooms no está habilitada para la cuenta
  - El usuario no es miembro de la sala de chat
  - Permisos insuficientes
- **404 Not Found**: Recurso no encontrado (sala, mensaje, usuario)
- **422 Unprocessable Entity**: Errores de validación

**Ejemplo de error:**
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

## Notas Adicionales

### Paginación en Mensajes

- Por defecto: 20 mensajes por página
- Máximo: 50 mensajes por página
- Los mensajes se retornan del más reciente al más antiguo
- Usa los headers de respuesta para información de paginación

### Estados de Mensaje

- `sent`: Mensaje enviado
- `delivered`: Mensaje entregado (todos los miembros han recibido notificación)
- `read`: Mensaje leído por todos los miembros (excepto el remitente)

### Adjuntos

- Soporta archivos múltiples por mensaje
- Usa `multipart/form-data` para enviar archivos
- Los archivos pueden ser imágenes, documentos, videos, etc.

### Respuestas a Mensajes

- Usa `content_attributes.in_reply_to` con el ID del mensaje original
- La API retorna los datos del mensaje original en el campo `in_reply_to`

### Permisos

- Solo los miembros de una sala pueden ver y enviar mensajes
- Solo administradores pueden ver todas las salas (listar)
- Los usuarios normales solo ven las salas de las que son miembros
- Solo administradores pueden crear/actualizar/eliminar salas
