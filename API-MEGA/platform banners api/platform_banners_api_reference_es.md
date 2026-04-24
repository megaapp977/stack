# Referencia de API de Platform Banners

## Descripción General

Platform Banners permite a los Super Admins mostrar mensajes importantes, alertas y anuncios a los usuarios de la plataforma. Los banners soportan formato markdown para contenido enriquecido.

## Características

- **Contenido Enriquecido**: Soporte para markdown (`**negrita**`, `*cursiva*`, `[enlace](url)`)
- **Tipos de Banner**: info, warning, error, success (con colores e iconos correspondientes)
- **Programación**: Establecer fechas de inicio y fin para banners temporales
- **Segmentación**: Mostrar banners a cuentas específicas o roles de usuario
- **Persistencia de Dismiss**: Los usuarios pueden cerrar banners y esto se guarda por usuario
- **Actualizaciones en Tiempo Real**: Los banners transmiten cambios vía ActionCable

---

## Platform API (para integraciones externas)

URL Base: `/platform/api/v1/platform_banners`

**Autenticación**: Requiere header `api_access_token` con un token válido de PlatformApp.

### Listar Todos los Banners

```http
GET /platform/api/v1/platform_banners
```

**Headers:**

```
api_access_token: TU_TOKEN_DE_PLATFORM_APP
```

**Respuesta (200 OK):**

```json
[
  {
    "id": 1,
    "title": "Mantenimiento Programado",
    "content": "Tendremos **mantenimiento programado** el viernes. [Ver estado](https://status.example.com)",
    "formatted_content": "Tendremos <strong>mantenimiento programado</strong> el viernes. <a href=\"https://status.example.com\" target=\"_blank\" rel=\"noopener noreferrer\">Ver estado</a>",
    "banner_type": "warning",
    "active": true,
    "starts_at": "2026-04-15T00:00:00Z",
    "ends_at": "2026-04-16T00:00:00Z",
    "status_url": null,
    "target_accounts": null,
    "target_user_roles": "all_users",
    "created_at": "2026-04-11T00:00:00Z",
    "updated_at": "2026-04-11T00:00:00Z"
  }
]
```

### Crear un Banner

```http
POST /platform/api/v1/platform_banners
```

**Headers:**

```
api_access_token: TU_TOKEN_DE_PLATFORM_APP
Content-Type: application/json
```

**Cuerpo de la Solicitud:**

```json
{
  "title": "Anuncio Importante",
  "content": "Estamos experimentando problemas con la **API de WhatsApp**. [Ver estado](https://metastatus.com)",
  "banner_type": "warning",
  "active": true,
  "starts_at": "2026-04-15T00:00:00Z",
  "ends_at": "2026-04-16T00:00:00Z",
  "target_accounts": [1, 2, 3],
  "target_user_roles": "all_users",
  "status_url": "https://status.example.com"
}
```

**Respuesta (201 Created):**

```json
{
  "id": 2,
  "title": "Anuncio Importante",
  "content": "Estamos experimentando problemas con la **API de WhatsApp**. [Ver estado](https://metastatus.com)",
  "formatted_content": "Estamos experimentando problemas con la <strong>API de WhatsApp</strong>. <a href=\"https://metastatus.com\" target=\"_blank\" rel=\"noopener noreferrer\">Ver estado</a>",
  "banner_type": "warning",
  "active": true,
  "starts_at": "2026-04-15T00:00:00Z",
  "ends_at": "2026-04-16T00:00:00Z",
  "status_url": "https://status.example.com",
  "target_accounts": [1, 2, 3],
  "target_user_roles": "all_users",
  "created_at": "2026-04-11T00:00:00Z",
  "updated_at": "2026-04-11T00:00:00Z"
}
```

### Obtener un Banner

```http
GET /platform/api/v1/platform_banners/:id
```

**Respuesta (200 OK):** Mismo objeto de banner individual.

### Actualizar un Banner

```http
PATCH /platform/api/v1/platform_banners/:id
```

**Cuerpo de la Solicitud:** (solo incluir campos a actualizar)

```json
{
  "title": "Título Actualizado",
  "banner_type": "error",
  "active": false
}
```

**Respuesta (200 OK):** Objeto del banner actualizado.

### Eliminar un Banner

```http
DELETE /platform/api/v1/platform_banners/:id
```

**Respuesta (200 OK):** Respuesta vacía.

---

## Account API (para usuarios del dashboard)

URL Base: `/api/v1/accounts/:account_id/platform_banners`

**Autenticación**: Requiere token de autenticación de usuario estándar.

### Listar Banners Activos para el Usuario

```http
GET /api/v1/accounts/:account_id/platform_banners
```

Retorna solo banners que:

- Están actualmente activos
- Coinciden con la cuenta del usuario
- Coinciden con el rol del usuario
- No han sido cerrados por el usuario

**Respuesta (200 OK):**

```json
[
  {
    "id": 1,
    "title": "Actualización del Sistema",
    "formatted_content": "Tenemos <strong>nuevas funciones</strong> disponibles!",
    "banner_type": "info",
    "status_url": null,
    "created_at": "2026-04-11T00:00:00Z",
    "updated_at": "2026-04-11T00:00:00Z"
  }
]
```

### Cerrar un Banner

```http
POST /api/v1/accounts/:account_id/platform_banners/:id/dismiss
```

Cierra un banner específico para el usuario actual. El banner no aparecerá de nuevo para este usuario.

**Respuesta (200 OK):** Respuesta vacía.

### Cerrar Todos los Banners

```http
POST /api/v1/accounts/:account_id/platform_banners/dismiss_all
```

Cierra todos los banners visibles actualmente para el usuario actual.

**Respuesta (200 OK):** Respuesta vacía.

---

## Modelo de Datos

### Campos del Banner

| Campo | Tipo | Descripción |
|-------|------|-------------|
| `id` | integer | Identificador único |
| `title` | string | Título del banner (requerido) |
| `content` | text | Contenido raw con soporte markdown (requerido) |
| `formatted_content` | string | Contenido formateado en HTML (solo lectura) |
| `banner_type` | enum | `info`, `warning`, `error`, `success` |
| `active` | boolean | Si el banner está activo (default: true) |
| `starts_at` | datetime | Cuándo empezar a mostrar (null = inmediatamente) |
| `ends_at` | datetime | Cuándo dejar de mostrar (null = indefinidamente) |
| `status_url` | string | URL adicional opcional de página de estado |
| `target_accounts` | array | IDs de cuentas objetivo (null = todas las cuentas) |
| `target_user_roles` | enum | `all_users`, `admin_only` |
| `created_at` | datetime | Fecha de creación |
| `updated_at` | datetime | Fecha de última actualización |

### Tipos de Banner

| Tipo | Color | Icono | Caso de Uso |
|------|-------|-------|-------------|
| `info` | Azul | ℹ️ | Anuncios generales, nuevas funciones |
| `warning` | Amarillo | ⚠️ | Mantenimiento próximo, problemas conocidos |
| `error` | Rojo | ❌ | Caídas críticas, problemas urgentes |
| `success` | Verde | ✅ | Problema resuelto, actualizaciones positivas |

---

## Soporte de Markdown

El campo `content` soporta formato markdown básico:

| Markdown | Resultado | Ejemplo |
|----------|-----------|---------|
| `**texto**` | **Negrita** | `**Importante**` → **Importante** |
| `*texto*` | *Cursiva* | `*Nota*` → *Nota* |
| `[texto](url)` | Enlace | `[Ver aquí](https://example.com)` → [Ver aquí](https://example.com) |

**Ejemplo de contenido:**

```
Estamos experimentando problemas con la **API de Meta**. Nuestro equipo está trabajando en ello. [Ver página de estado](https://status.example.com) para actualizaciones.
```

**Se renderiza como:**
> Estamos experimentando problemas con la **API de Meta**. Nuestro equipo está trabajando en ello. [Ver página de estado](https://status.example.com) para actualizaciones.

---

## Ejemplos de Uso

### Ejemplos con cURL

```bash
# Establecer tu token
TOKEN="TU_TOKEN_DE_PLATFORM_APP"

# Listar todos los banners
curl -s http://localhost:3000/platform/api/v1/platform_banners \
  -H "api_access_token: $TOKEN" | jq .

# Crear un banner de mantenimiento
curl -X POST http://localhost:3000/platform/api/v1/platform_banners \
  -H "api_access_token: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Mantenimiento Programado",
    "content": "Tendremos mantenimiento el **viernes a las 22:00**. [Página de estado](https://status.example.com)",
    "banner_type": "warning",
    "starts_at": "2026-04-15T00:00:00Z",
    "ends_at": "2026-04-16T00:00:00Z"
  }'

# Crear un banner de incidente
curl -X POST http://localhost:3000/platform/api/v1/platform_banners \
  -H "api_access_token: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Problemas con API de WhatsApp",
    "content": "Estamos experimentando problemas con la API de WhatsApp. **Los mensajes pueden retrasarse**. [Estado de Meta](https://metastatus.com)",
    "banner_type": "error"
  }'

# Actualizar banner a resuelto
curl -X PATCH http://localhost:3000/platform/api/v1/platform_banners/1 \
  -H "api_access_token: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Problemas con API de WhatsApp - RESUELTO",
    "content": "Los problemas con la API de WhatsApp han sido **resueltos**. ¡Gracias por su paciencia!",
    "banner_type": "success"
  }'

# Desactivar un banner
curl -X PATCH http://localhost:3000/platform/api/v1/platform_banners/1 \
  -H "api_access_token: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"active": false}'

# Eliminar un banner
curl -X DELETE http://localhost:3000/platform/api/v1/platform_banners/1 \
  -H "api_access_token: $TOKEN"
```

### Ejemplo con JavaScript/Axios

```javascript
import axios from 'axios';

const api = axios.create({
  baseURL: 'https://tu-instancia.com/platform/api/v1',
  headers: {
    'api_access_token': 'TU_TOKEN'
  }
});

// Crear banner
const banner = await api.post('/platform_banners', {
  title: 'Nueva Función Disponible',
  content: '¡Mira nuestro **nuevo dashboard**! [Saber más](https://docs.example.com)',
  banner_type: 'info'
});

// Actualizar banner
await api.patch(`/platform_banners/${banner.data.id}`, {
  banner_type: 'success'
});

// Eliminar banner
await api.delete(`/platform_banners/${banner.data.id}`);
```

---

## Actualizaciones en Tiempo Real

Los banners se transmiten vía ActionCable cuando se crean, actualizan o eliminan. El frontend actualiza automáticamente la lista de banners cuando se detectan cambios.

**Canal:** `PlatformBannersChannel`

---

## Dashboard de Super Admin

Los Super Admins también pueden gestionar banners vía la interfaz web en:

```
/super_admin/platform_banners
```

El dashboard proporciona:

- Lista de todos los banners con indicadores de estado
- Formularios de Crear/Editar con ayuda de markdown
- Filtrado por estado activo y tipo
- Activación/desactivación rápida

---

## Configuración

Los Platform Banners se controlan mediante un toggle de configuración respaldado en base de datos (`ENABLE_PLATFORM_BANNERS`), gestionado a través de `GlobalConfigService` y editable en el panel de **Super Admin** bajo App Config → General.

Cuando está deshabilitado:

- El endpoint index de la Account API retorna un array vacío (`[]`)
- Los endpoints dismiss/dismiss_all de la Account API retornan `404`
- Los endpoints de la Platform API retornan `404`
- El sidebar de Super Admin oculta la sección Platform Banners
