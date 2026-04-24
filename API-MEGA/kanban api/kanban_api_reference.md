# Referencia Completa de API Kanban

Esta guía mapea todas las APIs de Kanban/Funnel disponibles en el proyecto y documenta cada petición (método, ruta, parámetros y payloads clave).

## Autenticación

Todas las rutas de cuenta usan autenticación de usuario/API token.

Headers recomendados:

- `api_access_token: <TOKEN>`
- `Content-Type: application/json`

## Base URLs

- Account-scoped: `/api/v1/accounts/:account_id`
- Global (legacy): `/api/v1`

## Cambios implementados en este mapeo

- Nuevo endpoint: `GET /api/v1/accounts/:account_id/kanban_items/batch`
- Nuevo endpoint: `PATCH /api/v1/accounts/:account_id/funnels/:id/reorder`
- Nuevo filtro soportado en listados Kanban: `conversation_id`

---

## 1) Funnels

| Método | Endpoint | Parámetros | Descripción |
| --- | --- | --- | --- |
| GET | `/funnels` | - | Lista funneles de la cuenta |
| GET | `/funnels/:id` | `id` | Muestra un funnel |
| POST | `/funnels` | body `funnel` | Crea funnel |
| PATCH/PUT | `/funnels/:id` | body `funnel` | Actualiza funnel |
| DELETE | `/funnels/:id` | `id` | Elimina funnel y sus items |
| GET | `/funnels/:id/stage_stats` | filtros opcionales | Métricas por etapa |
| PATCH | `/funnels/:id/reorder` | body `stages[]` | Reordena etapas del funnel |
| GET | `/funnels/:funnel_id/kanban_items` | `funnel_id` | Lista items del funnel |

### Payload de creación/actualización de funnel

```json
{
  "funnel": {
    "name": "Ventas SMB",
    "description": "Pipeline comercial",
    "active": true,
    "is_default": false,
    "stages": {
      "lead": {
        "id": "lead",
        "name": "Lead",
        "color": "#94a3b8",
        "position": 1,
        "description": "Primer contacto"
      },
      "proposal": {
        "id": "proposal",
        "name": "Propuesta",
        "color": "#22c55e",
        "position": 2,
        "description": "Oferta enviada"
      }
    },
    "settings": {},
    "global_custom_attributes": []
  }
}
```

### Payload para reorder de etapas

```json
{
  "stages": ["proposal", "lead", "won"]
}
```

---

## 2) Kanban Items (core)

| Método | Endpoint | Parámetros | Descripción |
| --- | --- | --- | --- |
| GET | `/kanban_items` | `funnel_id`, `stage_id`, `agent_id`, `conversation_id`, `page` | Lista paginada de items |
| GET | `/kanban_items/batch` | mismos filtros de index | Lista + meta agregada (`stage_counts`, `total_items`) |
| GET | `/kanban_items/:id` | `id` | Detalle de item |
| POST | `/kanban_items` | body `kanban_item` | Crea item |
| PATCH/PUT | `/kanban_items/:id` | body `kanban_item` | Actualiza item |
| DELETE | `/kanban_items/:id` | `id` | Elimina item |

### Query de ejemplo (filtro por conversación)

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/kanban_items?conversation_id=12345" \
  -H "api_access_token: $API_TOKEN"
```

### Payload de creación/actualización de item

```json
{
  "kanban_item": {
    "funnel_id": 10,
    "funnel_stage": "lead",
    "position": 1,
    "conversation_display_id": 12345,
    "assigned_agents": [7, 11],
    "item_details": {
      "title": "Oportunidad ACME",
      "description": "Seguimiento comercial",
      "status": "open",
      "priority": "high",
      "value": 1500,
      "currency": {
        "symbol": "$",
        "code": "USD",
        "locale": "en"
      },
      "conversation_id": 12345,
      "notes": []
    }
  }
}
```

---

## 3) Movimiento y orden

| Método | Endpoint | Payload | Descripción |
| --- | --- | --- | --- |
| POST | `/kanban_items/:id/move_to_stage` | `funnel_stage`, opcional `funnel_id` | Mueve item de etapa |
| POST | `/kanban_items/:id/move` | `funnel_id`, `funnel_stage` | Mueve item de funnel/etapa |
| POST | `/kanban_items/reorder` | `positions[]` | Reordena items en tablero |

### Payload de reorder de items

```json
{
  "positions": [
    { "id": 101, "position": 1, "funnel_stage": "lead" },
    { "id": 102, "position": 2, "funnel_stage": "lead" }
  ]
}
```

---

## 4) Búsqueda, filtros y reportes

| Método | Endpoint | Parámetros | Descripción |
| --- | --- | --- | --- |
| GET | `/kanban_items/search` | `query`, `funnel_id`, `agent_id` | Búsqueda textual |
| GET | `/kanban_items/filter` | `funnel_id`, `priorities[]`, `value_min`, `value_max`, `agent_id`, rangos de fecha | Filtro avanzado |
| GET | `/kanban_items/reports` | `funnel_id`, `from`, `to`, `user_ids[]`, `inbox_id` | Métricas del tablero |
| GET | `/kanban_items/debug` | `funnel_id` | Debug técnico de items |

---

## 5) Checklist por item

| Método | Endpoint | Payload/Parámetros | Descripción |
| --- | --- | --- | --- |
| POST | `/kanban_items/:id/create_checklist_item` | `text`, `due_date`, `priority`, `agent_id` | Crea tarea checklist |
| GET | `/kanban_items/:id/get_checklist` | - | Lista checklist |
| PATCH | `/kanban_items/:id/update_checklist_item` | `checklist_item_id` + campos editables | Edita tarea |
| POST | `/kanban_items/:id/toggle_checklist_item` | `checklist_item_id` | Marca/desmarca completado |
| DELETE | `/kanban_items/:id/delete_checklist_item` | `checklist_item_id` | Elimina tarea |
| POST | `/kanban_items/:id/assign_agent_to_checklist_item` | `checklist_item_id`, `agent_id` | Asigna agente |
| DELETE | `/kanban_items/:id/remove_agent_from_checklist_item` | `checklist_item_id` | Quita agente |
| POST | `/kanban_items/:id/duplicate_checklist` | `target_item_id`, `merge` | Duplica checklist |
| GET | `/kanban_items/:id/search_checklist` | `query` | Busca en checklist |
| GET | `/kanban_items/:id/checklist_progress_by_agent` | - | Progreso por agente |

---

## 6) Notas por item

| Método | Endpoint | Payload/Parámetros | Descripción |
| --- | --- | --- | --- |
| POST | `/kanban_items/:id/create_note` | `text`, `attachments[]`, `linked_item_id`, `linked_conversation_id`, `linked_contact_id` | Crea nota |
| GET | `/kanban_items/:id/get_notes` | - | Lista notas |
| PATCH | `/kanban_items/:id/update_note` | `note_id` + campos editables | Edita nota |
| DELETE | `/kanban_items/:id/delete_note` | `note_id` | Elimina nota |

---

## 7) Adjuntos (item y nota)

| Método | Endpoint | Payload/Parámetros | Descripción |
| --- | --- | --- | --- |
| GET | `/kanban/items/:item_id/attachments` | - | Lista adjuntos del item |
| POST | `/kanban/items/:item_id/attachments` | multipart `attachment` | Sube adjunto al item |
| DELETE | `/kanban/items/:item_id/attachments/:id` | `id` | Elimina adjunto del item |
| POST | `/kanban/items/:item_id/note_attachments` | multipart `attachment` | Sube adjunto para notas |
| DELETE | `/kanban/items/:item_id/note_attachments/:id` | `id` | Elimina adjunto de nota |

---

## 8) Asignación, estado y tiempos

| Método | Endpoint | Payload/Parámetros | Descripción |
| --- | --- | --- | --- |
| POST | `/kanban_items/:id/assign_agent` | `agent_id` | Asigna agente al item |
| DELETE | `/kanban_items/:id/remove_agent` | `agent_id` | Quita agente del item |
| GET | `/kanban_items/:id/assigned_agents` | - | Lista agentes asignados |
| POST | `/kanban_items/:id/change_status` | `status` (`won`,`lost`,`open`) | Cambia estado comercial |
| GET | `/kanban_items/:id/time_report` | - | Tiempo acumulado del item |
| GET | `/kanban_items/:id/stage_time_breakdown` | - | Tiempo por etapa |
| GET | `/kanban_items/:id/counts` | - | Contadores (notas/checklist/adjuntos) |

---

## 9) Acciones masivas

| Método | Endpoint | Payload | Descripción |
| --- | --- | --- | --- |
| POST | `/kanban_items/bulk_move_items` | `item_ids[]`, `new_stage`, opcional `funnel_id` | Mueve varios items |
| POST | `/kanban_items/bulk_assign_agent` | `item_ids[]`, `agent_id`, `mode` (`replace`,`add`) | Asigna agente en lote |
| POST | `/kanban_items/bulk_set_priority` | `item_ids[]`, `priority` | Cambia prioridad en lote |

---

## 10) Importación y exportación CSV

| Método | Endpoint | Payload/Parámetros | Descripción |
| --- | --- | --- | --- |
| GET | `/kanban_items/export` | `funnel_id` + filtros opcionales | Exporta CSV |
| POST | `/kanban_items/import_preview` | multipart `file` | Vista previa de CSV |
| POST | `/kanban_items/import` | multipart `file`, `funnel_id`, `mappings`, opcional `default_stage_id` | Importa CSV |

---

## 11) Configuración de Kanban

| Método | Endpoint | Payload | Descripción |
| --- | --- | --- | --- |
| GET | `/kanban_config` | - | Obtiene configuración |
| POST | `/kanban_config` | body `kanban_config` | Crea configuración |
| PUT/PATCH | `/kanban_config` | body `kanban_config` | Actualiza configuración |
| DELETE | `/kanban_config` | - | Elimina configuración |
| POST | `/kanban_config/test_webhook` | - | Prueba webhook |

### Payload de configuración

```json
{
  "kanban_config": {
    "enabled": true,
    "webhook_url": "https://hooks.example.com/kanban",
    "webhook_secret": "secret",
    "webhook_events": ["kanban.item.created", "kanban.item.updated"],
    "config": {
      "title": "Mi Kanban",
      "default_view": "kanban",
      "auto_assignment": false,
      "notifications_enabled": true,
      "dragbar_enabled": true,
      "list_view_enabled": true,
      "agenda_view_enabled": true
    }
  }
}
```

---

## 12) Automatizaciones Kanban

### 12.1 Account-scoped (recomendado)

| Método | Endpoint | Payload | Descripción |
| --- | --- | --- | --- |
| GET | `/kanban/automations` | - | Lista automatizaciones |
| GET | `/kanban/automations/:id` | - | Muestra automatización |
| POST | `/kanban/automations` | body `kanban_automation` | Crea automatización |
| PATCH/PUT | `/kanban/automations/:id` | body `kanban_automation` | Actualiza automatización |
| DELETE | `/kanban/automations/:id` | - | Elimina automatización |

### 12.2 Global legacy (sin account scope)

| Método | Endpoint | Payload | Descripción |
| --- | --- | --- | --- |
| GET | `/api/v1/kanban_automations` | - | Lista global legacy |
| GET | `/api/v1/kanban_automations/:id` | - | Muestra global legacy |
| POST | `/api/v1/kanban_automations` | body `kanban_automation` | Crea global legacy |
| PATCH/PUT | `/api/v1/kanban_automations/:id` | body `kanban_automation` | Actualiza global legacy |
| DELETE | `/api/v1/kanban_automations/:id` | - | Elimina global legacy |

### 12.3 Namespace Kanban adicional

| Método | Endpoint | Payload/Parámetros | Descripción |
| --- | --- | --- | --- |
| GET | `/kanban/funnels` | - | Lista funnels por namespace Kanban |
| GET | `/kanban/funnels/:id` | `id` | Muestra funnel por namespace Kanban |
| POST | `/kanban/funnels` | body `funnel` | Crea funnel por namespace Kanban |
| PATCH/PUT | `/kanban/funnels/:id` | body `funnel` | Actualiza funnel por namespace Kanban |
| DELETE | `/kanban/funnels/:id` | `id` | Elimina funnel por namespace Kanban |
| GET | `/kanban/stages` | `funnel_id` | Lista etapas del funnel |
| GET | `/kanban/stages/:id` | opcional `funnel_id` | Muestra etapa por id |
| POST | `/kanban/stages` | `funnel_id`, body `stage` | Crea etapa |
| PATCH/PUT | `/kanban/stages/:id` | opcional `funnel_id`, body `stage` | Actualiza etapa |
| DELETE | `/kanban/stages/:id` | opcional `funnel_id`, opcional `fallback_stage_id` | Elimina etapa y mueve items |

---

## 13) Códigos de respuesta esperados

- `200 OK`: lectura/actualización exitosa
- `201 Created`: creación exitosa
- `204 No Content`: eliminación sin cuerpo
- `400 Bad Request`: payload o parámetros inválidos
- `401 Unauthorized`: token inválido/faltante
- `403 Forbidden`: sin permisos/licencia
- `404 Not Found`: recurso inexistente
- `422 Unprocessable Entity`: validaciones de negocio
- `500 Internal Server Error`: error inesperado
