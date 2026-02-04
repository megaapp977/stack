# API de Mensajes Agendados - Referencia

Esta documentación proporciona ejemplos de uso de la API de Mensajes Agendados usando curl.

## Autenticación

Todas las peticiones requieren autenticación mediante token de API. Debes incluir el header `api_access_token` en cada petición.

```bash
# Configurar variables de entorno
export API_TOKEN="tu_token_de_api"
export ACCOUNT_ID="1"
export BASE_URL="http://localhost:3000"
```

---

## Mensajes Agendados (Account Level)

### 1. Listar Mensajes Agendados

Lista todos los mensajes agendados de la cuenta, ordenados por fecha de programación descendente.

**Endpoint:** `GET /api/v1/accounts/:account_id/scheduled_messages`

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Respuesta de ejemplo:**

```json
{
  "payload": [
    {
      "id": 1,
      "content": "Recordatorio: Reunión mañana a las 10 AM",
      "scheduled_at": 1738836000,
      "sent_at": null,
      "title": "Recordatorio de reunión",
      "inbox_id": 5,
      "inbox_name": "WhatsApp Business",
      "conversation_id": 123,
      "contact_id": 456,
      "contact_name": "Juan Pérez",
      "contact_phone": "+5491112345678",
      "contact_email": "juan@example.com",
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
      "assignee_name": "María García",
      "assignee_avatar_url": "https://example.com/avatar.png"
    }
  ]
}
```

**Estados posibles:**

- `pending`: Mensaje en espera de ser enviado
- `sent`: Mensaje enviado exitosamente
- `failed`: El envío falló

---

### 2. Ver Mensaje Agendado

Obtiene los detalles de un mensaje agendado específico.

**Endpoint:** `GET /api/v1/accounts/:account_id/scheduled_messages/:id`

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages/1" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Respuesta:** Igual estructura que un elemento del listado.

---

### 3. Crear Mensaje Agendado

Crea un nuevo mensaje agendado a nivel de cuenta.

**Endpoint:** `POST /api/v1/accounts/:account_id/scheduled_messages`

#### 3.1 Mensaje Simple

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Hola, este es un mensaje agendado",
    "scheduled_at": "2026-02-06T15:00:00Z",
    "title": "Seguimiento al cliente"
  }'
```

#### 3.2 Mensaje con Adjuntos

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -F "inbox_id=5" \
  -F "contact_id=456" \
  -F "content=Adjunto el documento solicitado" \
  -F "scheduled_at=2026-02-06T15:00:00Z" \
  -F "title=Envío de documento" \
  -F "attachments[]=@/ruta/al/documento.pdf" \
  -F "attachments[]=@/ruta/a/imagen.jpg"
```

**Límite:** Máximo 15 adjuntos por mensaje.

#### 3.3 Mensaje con Template de WhatsApp

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Plantilla de confirmación",
    "scheduled_at": "2026-02-06T15:00:00Z",
    "title": "Confirmar cita",
    "template_params": {
      "name": "appointment_reminder",
      "category": "UTILITY",
      "language": "es",
      "namespace": "tu_namespace",
      "processed_params": {
        "header": {},
        "body": [
          {"type": "text", "text": "Juan Pérez"},
          {"type": "text", "text": "10:00 AM"},
          {"type": "text", "text": "6 de febrero"}
        ],
        "buttons": []
      }
    }
  }'
```

#### 3.4 Mensaje Recurrente

```bash
# Mensaje diario que se repite 10 veces
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Recordatorio diario",
    "scheduled_at": "2026-02-06T09:00:00Z",
    "title": "Recordatorio matutino",
    "recurrence_type": "daily",
    "recurrence_interval": 1,
    "recurrence_end_type": "after_occurrences",
    "recurrence_max_occurrences": 10
  }'
```

```bash
# Mensaje semanal que se repite hasta una fecha
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Reporte semanal",
    "scheduled_at": "2026-02-10T10:00:00Z",
    "title": "Reporte ejecutivo",
    "recurrence_type": "weekly",
    "recurrence_interval": 1,
    "recurrence_days": [1],
    "recurrence_end_type": "on_date",
    "recurrence_end_date": "2026-12-31"
  }'
```

```bash
# Mensaje mensual infinito
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Recordatorio mensual",
    "scheduled_at": "2026-03-01T12:00:00Z",
    "title": "Seguimiento mensual",
    "recurrence_type": "monthly",
    "recurrence_interval": 1,
    "recurrence_end_type": "never"
  }'
```

**Parámetros de recurrencia:**

- `recurrence_type`: `none` (default), `daily`, `weekly`, `monthly`, `yearly`
- `recurrence_interval`: Intervalo de repetición (ej: 2 = cada 2 días/semanas/meses)
- `recurrence_days`: Array de días de la semana (0=Domingo, 6=Sábado) - Solo para `weekly`
- `recurrence_end_type`: `never`, `on_date`, `after_occurrences`
- `recurrence_end_date`: Fecha hasta la cual repetir (ISO 8601) - Requerido si `recurrence_end_type` es `on_date`
- `recurrence_max_occurrences`: Número máximo de ocurrencias - Requerido si `recurrence_end_type` es `after_occurrences`

**Respuesta de ejemplo:**

```json
{
  "id": 2,
  "content": "Hola, este es un mensaje agendado",
  "scheduled_at": 1738854000,
  "sent_at": null,
  "title": "Seguimiento al cliente",
  "inbox_id": 5,
  "inbox_name": "WhatsApp Business",
  "conversation_id": null,
  "contact_id": 456,
  "contact_name": "Juan Pérez",
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

### 4. Actualizar Mensaje Agendado

Actualiza un mensaje agendado existente. Solo se pueden actualizar mensajes con estado `pending`.

**Endpoint:** `PUT /api/v1/accounts/:account_id/scheduled_messages/:id`

```bash
curl -X PUT \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages/1" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "content": "Mensaje actualizado",
    "scheduled_at": "2026-02-07T16:00:00Z",
    "title": "Título actualizado"
  }'
```

**Nota:** El campo `status` no puede ser modificado manualmente. Se actualiza automáticamente cuando el mensaje es enviado o falla.

---

### 5. Eliminar Mensaje Agendado

Elimina un mensaje agendado. Se puede eliminar en cualquier estado.

**Endpoint:** `DELETE /api/v1/accounts/:account_id/scheduled_messages/:id`

```bash
curl -X DELETE \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages/1" \
  -H "api_access_token: $API_TOKEN"
```

**Respuesta:** `204 No Content`

---

## Mensajes Agendados por Conversación

### 1. Listar Mensajes de una Conversación

Lista todos los mensajes agendados asociados a un contacto específico (incluye todas sus conversaciones).

**Endpoint:** `GET /api/v1/accounts/:account_id/conversations/:conversation_id/scheduled_messages`

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Respuesta de ejemplo:**

```json
{
  "payload": [
    {
      "id": 1,
      "content": "Seguimiento programado",
      "scheduled_at": 1738836000,
      "sent_at": null,
      "title": "Seguimiento",
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

### 2. Ver Mensaje Agendado

Obtiene los detalles de un mensaje agendado específico.

**Endpoint:** `GET /api/v1/accounts/:account_id/conversations/:conversation_id/scheduled_messages/:id`

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages/1" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

---

### 3. Crear Mensaje Agendado en Conversación

Crea un mensaje agendado dentro de una conversación existente.

**Endpoint:** `POST /api/v1/accounts/:account_id/conversations/:conversation_id/scheduled_messages`

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "scheduled_message": {
      "content": "Este es un mensaje agendado desde la conversación",
      "scheduled_at": "2026-02-06T15:00:00Z",
      "title": "Seguimiento automático",
      "inbox_id": 5
    }
  }'
```

**Con adjuntos:**

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -F "scheduled_message[content]=Mensaje con archivo" \
  -F "scheduled_message[scheduled_at]=2026-02-06T15:00:00Z" \
  -F "scheduled_message[title]=Envío de documento" \
  -F "scheduled_message[inbox_id]=5" \
  -F "scheduled_message[attachments][]=@/ruta/al/archivo.pdf"
```

---

### 4. Actualizar Mensaje Agendado

Actualiza un mensaje agendado en una conversación.

**Endpoint:** `PUT /api/v1/accounts/:account_id/conversations/:conversation_id/scheduled_messages/:id`

```bash
curl -X PUT \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages/1" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "scheduled_message": {
      "content": "Mensaje actualizado desde conversación",
      "scheduled_at": "2026-02-07T16:00:00Z"
    }
  }'
```

---

### 5. Eliminar Mensaje Agendado

Elimina un mensaje agendado de una conversación.

**Endpoint:** `DELETE /api/v1/accounts/:account_id/conversations/:conversation_id/scheduled_messages/:id`

```bash
curl -X DELETE \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages/1" \
  -H "api_access_token: $API_TOKEN"
```

**Respuesta:** `200 OK`

---

### 6. Contar Mensajes Agendados

Cuenta los mensajes agendados de una conversación, con opción de filtrar por estado.

**Endpoint:** `GET /api/v1/accounts/:account_id/conversations/:conversation_id/scheduled_messages/count`

```bash
# Contar todos los mensajes
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages/count" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"

# Contar mensajes pendientes
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages/count?status=pending" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Respuesta:**

```json
{
  "count": 5
}
```

---

## Casos de Uso Comunes

### 1. Seguimiento Automático Post-Venta

```bash
# Agendar mensaje de seguimiento 24 horas después
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Hola, ¿cómo estuvo tu experiencia con nuestro producto?",
    "scheduled_at": "2026-02-07T10:00:00Z",
    "title": "Seguimiento post-venta"
  }'
```

### 2. Recordatorios de Citas

```bash
# Recordatorio 1 día antes
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Recordatorio: Tienes una cita mañana a las 15:00",
    "scheduled_at": "2026-02-09T09:00:00Z",
    "title": "Recordatorio de cita"
  }'
```

### 3. Newsletters Semanales

```bash
# Newsletter cada lunes a las 9 AM
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "¡Buenos días! Aquí está tu newsletter semanal",
    "scheduled_at": "2026-02-10T09:00:00Z",
    "title": "Newsletter Semanal",
    "recurrence_type": "weekly",
    "recurrence_interval": 1,
    "recurrence_days": [1],
    "recurrence_end_type": "never"
  }'
```

### 4. Campaña de Nutrición (Lead Nurturing)

```bash
# Mensaje 1: Inmediato
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 789,
    "content": "¡Gracias por tu interés! Aquí tienes más información...",
    "scheduled_at": "2026-02-06T10:00:00Z",
    "title": "Campaña - Día 0"
  }'

# Mensaje 2: 3 días después
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 789,
    "content": "¿Has tenido oportunidad de revisar la información?",
    "scheduled_at": "2026-02-09T10:00:00Z",
    "title": "Campaña - Día 3"
  }'

# Mensaje 3: 7 días después
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 789,
    "content": "Oferta especial disponible solo por tiempo limitado",
    "scheduled_at": "2026-02-13T10:00:00Z",
    "title": "Campaña - Día 7"
  }'
```

---

## Permisos

### Edición Estándar (OSS)

Los permisos están controlados por la política `ScheduledMessagePolicy`:

- **Administradores**: Acceso completo
- **Agentes**: Pueden gestionar sus propios mensajes agendados
- **Supervisor de inbox**: Puede gestionar mensajes del inbox que supervisa

### Enterprise Edition

En la edición Enterprise, se puede asignar el permiso granular:

- `scheduled_message_manage`: Permite gestionar todos los mensajes agendados de la cuenta

Este permiso puede asignarse a roles personalizados (Custom Roles).

---

## Notas Importantes

1. **Zona Horaria**: Todas las fechas deben enviarse en formato ISO 8601 (UTC). El sistema las convertirá según la zona horaria de la cuenta.

2. **Validación de Fecha**: No se puede agendar un mensaje en el pasado.

3. **Límite de Adjuntos**: Máximo 15 archivos por mensaje.

4. **Estados**:
   - Los mensajes se crean con estado `pending`
   - Cambian a `sent` cuando se envían exitosamente
   - Cambian a `failed` si hay un error en el envío

5. **Job Asíncrono**: Los mensajes se envían mediante `ScheduledMessageJob` que se ejecuta en la fecha/hora programada.

6. **Recurrencia**:
   - Los mensajes recurrentes crean automáticamente la siguiente ocurrencia después de enviarse
   - Se puede detener la recurrencia eliminando el mensaje padre
   - El campo `parent_id` indica si es una ocurrencia de un mensaje recurrente

7. **Templates de WhatsApp**:
   - Los templates deben estar previamente aprobados en WhatsApp Business API
   - Los parámetros deben coincidir exactamente con la estructura del template

8. **Eliminación**:
   - Eliminar un mensaje `pending` cancela su envío
   - Eliminar un mensaje recurrente padre detiene todas las futuras ocurrencias

---

## Códigos de Error Comunes

- `404 Not Found`: El mensaje agendado no existe o no pertenece a la cuenta
- `422 Unprocessable Entity`: Errores de validación (fecha inválida, campos requeridos, etc.)
- `403 Forbidden`: Sin permisos para realizar la acción

**Ejemplos de errores:**

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

## Webhook Events

El sistema emite los siguientes eventos para mensajes agendados:

- `scheduled_message.created`: Cuando se crea un mensaje agendado
- `scheduled_message.updated`: Cuando se actualiza un mensaje agendado
- `scheduled_message.deleted`: Cuando se elimina un mensaje agendado

Estos eventos se pueden capturar mediante webhooks configurados en la cuenta.

---
