# Complete Kanban API Reference

This guide maps all available Kanban/Funnel APIs and documents each request (method, path, parameters, and key payloads).

## Authentication

All account routes use user/API token authentication.

Recommended headers:

- `api_access_token: <TOKEN>`
- `Content-Type: application/json`

## Base URLs

- Account-scoped: `/api/v1/accounts/:account_id`
- Global (legacy): `/api/v1`

## Changes implemented in this mapping

- New endpoint: `GET /api/v1/accounts/:account_id/kanban_items/batch`
- New endpoint: `PATCH /api/v1/accounts/:account_id/funnels/:id/reorder`
- New supported filter on Kanban list endpoints: `conversation_id`

---

## 1) Funnels

| Method | Endpoint | Parameters | Description |
| --- | --- | --- | --- |
| GET | `/funnels` | - | List account funnels |
| GET | `/funnels/:id` | `id` | Show funnel |
| POST | `/funnels` | body `funnel` | Create funnel |
| PATCH/PUT | `/funnels/:id` | body `funnel` | Update funnel |
| DELETE | `/funnels/:id` | `id` | Delete funnel and related items |
| GET | `/funnels/:id/stage_stats` | optional filters | Stage metrics |
| PATCH | `/funnels/:id/reorder` | body `stages[]` | Reorder funnel stages |
| GET | `/funnels/:funnel_id/kanban_items` | `funnel_id` | List funnel items |

### Funnel create/update payload

```json
{
  "funnel": {
    "name": "SMB Sales",
    "description": "Commercial pipeline",
    "active": true,
    "is_default": false,
    "stages": {
      "lead": {
        "id": "lead",
        "name": "Lead",
        "color": "#94a3b8",
        "position": 1,
        "description": "First contact"
      },
      "proposal": {
        "id": "proposal",
        "name": "Proposal",
        "color": "#22c55e",
        "position": 2,
        "description": "Offer sent"
      }
    },
    "settings": {},
    "global_custom_attributes": []
  }
}
```

### Stage reorder payload

```json
{
  "stages": ["proposal", "lead", "won"]
}
```

---

## 2) Kanban Items (core)

| Method | Endpoint | Parameters | Description |
| --- | --- | --- | --- |
| GET | `/kanban_items` | `funnel_id`, `stage_id`, `agent_id`, `conversation_id`, `page` | Paginated list |
| GET | `/kanban_items/batch` | same filters as index | List + aggregated meta (`stage_counts`, `total_items`) |
| GET | `/kanban_items/:id` | `id` | Item details |
| POST | `/kanban_items` | body `kanban_item` | Create item |
| PATCH/PUT | `/kanban_items/:id` | body `kanban_item` | Update item |
| DELETE | `/kanban_items/:id` | `id` | Delete item |

### Query example (conversation filter)

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/kanban_items?conversation_id=12345" \
  -H "api_access_token: $API_TOKEN"
```

### Item create/update payload

```json
{
  "kanban_item": {
    "funnel_id": 10,
    "funnel_stage": "lead",
    "position": 1,
    "conversation_display_id": 12345,
    "assigned_agents": [7, 11],
    "item_details": {
      "title": "ACME Opportunity",
      "description": "Sales follow-up",
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

## 3) Movement and ordering

| Method | Endpoint | Payload | Description |
| --- | --- | --- | --- |
| POST | `/kanban_items/:id/move_to_stage` | `funnel_stage`, optional `funnel_id` | Move item to another stage |
| POST | `/kanban_items/:id/move` | `funnel_id`, `funnel_stage` | Move item across funnel/stage |
| POST | `/kanban_items/reorder` | `positions[]` | Reorder board items |

### Item reorder payload

```json
{
  "positions": [
    { "id": 101, "position": 1, "funnel_stage": "lead" },
    { "id": 102, "position": 2, "funnel_stage": "lead" }
  ]
}
```

---

## 4) Search, filters, reports

| Method | Endpoint | Parameters | Description |
| --- | --- | --- | --- |
| GET | `/kanban_items/search` | `query`, `funnel_id`, `agent_id` | Text search |
| GET | `/kanban_items/filter` | `funnel_id`, `priorities[]`, `value_min`, `value_max`, `agent_id`, date ranges | Advanced filtering |
| GET | `/kanban_items/reports` | `funnel_id`, `from`, `to`, `user_ids[]`, `inbox_id` | Board metrics |
| GET | `/kanban_items/debug` | `funnel_id` | Technical debug data |

---

## 5) Checklist per item

| Method | Endpoint | Payload/Parameters | Description |
| --- | --- | --- | --- |
| POST | `/kanban_items/:id/create_checklist_item` | `text`, `due_date`, `priority`, `agent_id` | Create checklist task |
| GET | `/kanban_items/:id/get_checklist` | - | List checklist |
| PATCH | `/kanban_items/:id/update_checklist_item` | `checklist_item_id` + editable fields | Update checklist task |
| POST | `/kanban_items/:id/toggle_checklist_item` | `checklist_item_id` | Toggle completion |
| DELETE | `/kanban_items/:id/delete_checklist_item` | `checklist_item_id` | Delete checklist task |
| POST | `/kanban_items/:id/assign_agent_to_checklist_item` | `checklist_item_id`, `agent_id` | Assign checklist task |
| DELETE | `/kanban_items/:id/remove_agent_from_checklist_item` | `checklist_item_id` | Remove assigned agent |
| POST | `/kanban_items/:id/duplicate_checklist` | `target_item_id`, `merge` | Duplicate checklist |
| GET | `/kanban_items/:id/search_checklist` | `query` | Search checklist |
| GET | `/kanban_items/:id/checklist_progress_by_agent` | - | Progress by agent |

---

## 6) Notes per item

| Method | Endpoint | Payload/Parameters | Description |
| --- | --- | --- | --- |
| POST | `/kanban_items/:id/create_note` | `text`, `attachments[]`, `linked_item_id`, `linked_conversation_id`, `linked_contact_id` | Create note |
| GET | `/kanban_items/:id/get_notes` | - | List notes |
| PATCH | `/kanban_items/:id/update_note` | `note_id` + editable fields | Update note |
| DELETE | `/kanban_items/:id/delete_note` | `note_id` | Delete note |

---

## 7) Attachments (item and note)

| Method | Endpoint | Payload/Parameters | Description |
| --- | --- | --- | --- |
| GET | `/kanban/items/:item_id/attachments` | - | List item attachments |
| POST | `/kanban/items/:item_id/attachments` | multipart `attachment` | Upload item attachment |
| DELETE | `/kanban/items/:item_id/attachments/:id` | `id` | Delete item attachment |
| POST | `/kanban/items/:item_id/note_attachments` | multipart `attachment` | Upload note attachment |
| DELETE | `/kanban/items/:item_id/note_attachments/:id` | `id` | Delete note attachment |

---

## 8) Assignment, status, timing

| Method | Endpoint | Payload/Parameters | Description |
| --- | --- | --- | --- |
| POST | `/kanban_items/:id/assign_agent` | `agent_id` | Assign agent |
| DELETE | `/kanban_items/:id/remove_agent` | `agent_id` | Remove agent |
| GET | `/kanban_items/:id/assigned_agents` | - | List assigned agents |
| POST | `/kanban_items/:id/change_status` | `status` (`won`,`lost`,`open`) | Change commercial status |
| GET | `/kanban_items/:id/time_report` | - | Item time report |
| GET | `/kanban_items/:id/stage_time_breakdown` | - | Time per stage |
| GET | `/kanban_items/:id/counts` | - | Counters (notes/checklist/attachments) |

---

## 9) Bulk actions

| Method | Endpoint | Payload | Description |
| --- | --- | --- | --- |
| POST | `/kanban_items/bulk_move_items` | `item_ids[]`, `new_stage`, optional `funnel_id` | Move multiple items |
| POST | `/kanban_items/bulk_assign_agent` | `item_ids[]`, `agent_id`, `mode` (`replace`,`add`) | Bulk assign agent |
| POST | `/kanban_items/bulk_set_priority` | `item_ids[]`, `priority` | Bulk priority update |

---

## 10) CSV import/export

| Method | Endpoint | Payload/Parameters | Description |
| --- | --- | --- | --- |
| GET | `/kanban_items/export` | `funnel_id` + optional filters | Export CSV |
| POST | `/kanban_items/import_preview` | multipart `file` | CSV preview |
| POST | `/kanban_items/import` | multipart `file`, `funnel_id`, `mappings`, optional `default_stage_id` | Import CSV |

---

## 11) Kanban configuration

| Method | Endpoint | Payload | Description |
| --- | --- | --- | --- |
| GET | `/kanban_config` | - | Read configuration |
| POST | `/kanban_config` | body `kanban_config` | Create configuration |
| PUT/PATCH | `/kanban_config` | body `kanban_config` | Update configuration |
| DELETE | `/kanban_config` | - | Delete configuration |
| POST | `/kanban_config/test_webhook` | - | Test webhook |

### Configuration payload

```json
{
  "kanban_config": {
    "enabled": true,
    "webhook_url": "https://hooks.example.com/kanban",
    "webhook_secret": "secret",
    "webhook_events": ["kanban.item.created", "kanban.item.updated"],
    "config": {
      "title": "My Kanban",
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

## 12) Kanban automations

### 12.1 Account-scoped (recommended)

| Method | Endpoint | Payload | Description |
| --- | --- | --- | --- |
| GET | `/kanban/automations` | - | List automations |
| GET | `/kanban/automations/:id` | - | Show automation |
| POST | `/kanban/automations` | body `kanban_automation` | Create automation |
| PATCH/PUT | `/kanban/automations/:id` | body `kanban_automation` | Update automation |
| DELETE | `/kanban/automations/:id` | - | Delete automation |

### 12.2 Global legacy (non account-scoped)

| Method | Endpoint | Payload | Description |
| --- | --- | --- | --- |
| GET | `/api/v1/kanban_automations` | - | Global legacy list |
| GET | `/api/v1/kanban_automations/:id` | - | Global legacy detail |
| POST | `/api/v1/kanban_automations` | body `kanban_automation` | Create legacy record |
| PATCH/PUT | `/api/v1/kanban_automations/:id` | body `kanban_automation` | Update legacy record |
| DELETE | `/api/v1/kanban_automations/:id` | - | Delete legacy record |

### 12.3 Additional Kanban namespace

| Method | Endpoint | Payload/Parameters | Description |
| --- | --- | --- | --- |
| GET | `/kanban/funnels` | - | List funnels via Kanban namespace |
| GET | `/kanban/funnels/:id` | `id` | Show funnel via Kanban namespace |
| POST | `/kanban/funnels` | body `funnel` | Create funnel via Kanban namespace |
| PATCH/PUT | `/kanban/funnels/:id` | body `funnel` | Update funnel via Kanban namespace |
| DELETE | `/kanban/funnels/:id` | `id` | Delete funnel via Kanban namespace |
| GET | `/kanban/stages` | `funnel_id` | List funnel stages |
| GET | `/kanban/stages/:id` | optional `funnel_id` | Show stage by id |
| POST | `/kanban/stages` | `funnel_id`, body `stage` | Create stage |
| PATCH/PUT | `/kanban/stages/:id` | optional `funnel_id`, body `stage` | Update stage |
| DELETE | `/kanban/stages/:id` | optional `funnel_id`, optional `fallback_stage_id` | Delete stage and move items |

---

## 13) Expected response codes

- `200 OK`: successful read/update
- `201 Created`: successful creation
- `204 No Content`: delete without body
- `400 Bad Request`: invalid payload/params
- `401 Unauthorized`: missing/invalid token
- `403 Forbidden`: no permission/license
- `404 Not Found`: resource not found
- `422 Unprocessable Entity`: business validation errors
- `500 Internal Server Error`: unexpected error
