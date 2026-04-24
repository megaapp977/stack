# Referência Completa da API Kanban

Este guia mapeia todas as APIs de Kanban/Funnel disponíveis e documenta cada requisição (método, rota, parâmetros e payloads principais).

## Autenticação

Todas as rotas de conta usam autenticação por token de usuário/API.

Headers recomendados:

- `api_access_token: <TOKEN>`
- `Content-Type: application/json`

## Base URLs

- Escopo de conta: `/api/v1/accounts/:account_id`
- Global (legado): `/api/v1`

## Mudanças implementadas neste mapeamento

- Novo endpoint: `GET /api/v1/accounts/:account_id/kanban_items/batch`
- Novo endpoint: `PATCH /api/v1/accounts/:account_id/funnels/:id/reorder`
- Novo filtro suportado em listagens Kanban: `conversation_id`

---

## 1) Funnels

| Método | Endpoint | Parâmetros | Descrição |
| --- | --- | --- | --- |
| GET | `/funnels` | - | Lista funis da conta |
| GET | `/funnels/:id` | `id` | Exibe funil |
| POST | `/funnels` | body `funnel` | Cria funil |
| PATCH/PUT | `/funnels/:id` | body `funnel` | Atualiza funil |
| DELETE | `/funnels/:id` | `id` | Remove funil e itens relacionados |
| GET | `/funnels/:id/stage_stats` | filtros opcionais | Métricas por etapa |
| PATCH | `/funnels/:id/reorder` | body `stages[]` | Reordena etapas do funil |
| GET | `/funnels/:funnel_id/kanban_items` | `funnel_id` | Lista itens do funil |

### Payload de criação/atualização de funil

```json
{
  "funnel": {
    "name": "Vendas SMB",
    "description": "Pipeline comercial",
    "active": true,
    "is_default": false,
    "stages": {
      "lead": {
        "id": "lead",
        "name": "Lead",
        "color": "#94a3b8",
        "position": 1,
        "description": "Primeiro contato"
      },
      "proposal": {
        "id": "proposal",
        "name": "Proposta",
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

| Método | Endpoint | Parâmetros | Descrição |
| --- | --- | --- | --- |
| GET | `/kanban_items` | `funnel_id`, `stage_id`, `agent_id`, `conversation_id`, `page` | Lista paginada |
| GET | `/kanban_items/batch` | mesmos filtros do index | Lista + metadados agregados (`stage_counts`, `total_items`) |
| GET | `/kanban_items/:id` | `id` | Detalhe do item |
| POST | `/kanban_items` | body `kanban_item` | Cria item |
| PATCH/PUT | `/kanban_items/:id` | body `kanban_item` | Atualiza item |
| DELETE | `/kanban_items/:id` | `id` | Exclui item |

### Exemplo de query (filtro por conversa)

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/kanban_items?conversation_id=12345" \
  -H "api_access_token: $API_TOKEN"
```

### Payload de criação/atualização de item

```json
{
  "kanban_item": {
    "funnel_id": 10,
    "funnel_stage": "lead",
    "position": 1,
    "conversation_display_id": 12345,
    "assigned_agents": [7, 11],
    "item_details": {
      "title": "Oportunidade ACME",
      "description": "Follow-up comercial",
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

## 3) Movimentação e ordenação

| Método | Endpoint | Payload | Descrição |
| --- | --- | --- | --- |
| POST | `/kanban_items/:id/move_to_stage` | `funnel_stage`, opcional `funnel_id` | Move item para outra etapa |
| POST | `/kanban_items/:id/move` | `funnel_id`, `funnel_stage` | Move item entre funil/etapa |
| POST | `/kanban_items/reorder` | `positions[]` | Reordena itens no quadro |

### Payload de reorder de itens

```json
{
  "positions": [
    { "id": 101, "position": 1, "funnel_stage": "lead" },
    { "id": 102, "position": 2, "funnel_stage": "lead" }
  ]
}
```

---

## 4) Busca, filtros e relatórios

| Método | Endpoint | Parâmetros | Descrição |
| --- | --- | --- | --- |
| GET | `/kanban_items/search` | `query`, `funnel_id`, `agent_id` | Busca textual |
| GET | `/kanban_items/filter` | `funnel_id`, `priorities[]`, `value_min`, `value_max`, `agent_id`, intervalos de data | Filtro avançado |
| GET | `/kanban_items/reports` | `funnel_id`, `from`, `to`, `user_ids[]`, `inbox_id` | Métricas do quadro |
| GET | `/kanban_items/debug` | `funnel_id` | Dados técnicos de debug |

---

## 5) Checklist por item

| Método | Endpoint | Payload/Parâmetros | Descrição |
| --- | --- | --- | --- |
| POST | `/kanban_items/:id/create_checklist_item` | `text`, `due_date`, `priority`, `agent_id` | Cria tarefa de checklist |
| GET | `/kanban_items/:id/get_checklist` | - | Lista checklist |
| PATCH | `/kanban_items/:id/update_checklist_item` | `checklist_item_id` + campos editáveis | Atualiza tarefa |
| POST | `/kanban_items/:id/toggle_checklist_item` | `checklist_item_id` | Marca/desmarca conclusão |
| DELETE | `/kanban_items/:id/delete_checklist_item` | `checklist_item_id` | Exclui tarefa |
| POST | `/kanban_items/:id/assign_agent_to_checklist_item` | `checklist_item_id`, `agent_id` | Atribui agente |
| DELETE | `/kanban_items/:id/remove_agent_from_checklist_item` | `checklist_item_id` | Remove agente |
| POST | `/kanban_items/:id/duplicate_checklist` | `target_item_id`, `merge` | Duplica checklist |
| GET | `/kanban_items/:id/search_checklist` | `query` | Busca no checklist |
| GET | `/kanban_items/:id/checklist_progress_by_agent` | - | Progresso por agente |

---

## 6) Notas por item

| Método | Endpoint | Payload/Parâmetros | Descrição |
| --- | --- | --- | --- |
| POST | `/kanban_items/:id/create_note` | `text`, `attachments[]`, `linked_item_id`, `linked_conversation_id`, `linked_contact_id` | Cria nota |
| GET | `/kanban_items/:id/get_notes` | - | Lista notas |
| PATCH | `/kanban_items/:id/update_note` | `note_id` + campos editáveis | Atualiza nota |
| DELETE | `/kanban_items/:id/delete_note` | `note_id` | Exclui nota |

---

## 7) Anexos (item e nota)

| Método | Endpoint | Payload/Parâmetros | Descrição |
| --- | --- | --- | --- |
| GET | `/kanban/items/:item_id/attachments` | - | Lista anexos do item |
| POST | `/kanban/items/:item_id/attachments` | multipart `attachment` | Envia anexo do item |
| DELETE | `/kanban/items/:item_id/attachments/:id` | `id` | Exclui anexo do item |
| POST | `/kanban/items/:item_id/note_attachments` | multipart `attachment` | Envia anexo de nota |
| DELETE | `/kanban/items/:item_id/note_attachments/:id` | `id` | Exclui anexo de nota |

---

## 8) Atribuição, status e tempo

| Método | Endpoint | Payload/Parâmetros | Descrição |
| --- | --- | --- | --- |
| POST | `/kanban_items/:id/assign_agent` | `agent_id` | Atribui agente |
| DELETE | `/kanban_items/:id/remove_agent` | `agent_id` | Remove agente |
| GET | `/kanban_items/:id/assigned_agents` | - | Lista agentes atribuídos |
| POST | `/kanban_items/:id/change_status` | `status` (`won`,`lost`,`open`) | Altera status comercial |
| GET | `/kanban_items/:id/time_report` | - | Relatório de tempo do item |
| GET | `/kanban_items/:id/stage_time_breakdown` | - | Tempo por etapa |
| GET | `/kanban_items/:id/counts` | - | Contadores (notas/checklist/anexos) |

---

## 9) Ações em massa

| Método | Endpoint | Payload | Descrição |
| --- | --- | --- | --- |
| POST | `/kanban_items/bulk_move_items` | `item_ids[]`, `new_stage`, opcional `funnel_id` | Move múltiplos itens |
| POST | `/kanban_items/bulk_assign_agent` | `item_ids[]`, `agent_id`, `mode` (`replace`,`add`) | Atribui agente em lote |
| POST | `/kanban_items/bulk_set_priority` | `item_ids[]`, `priority` | Atualiza prioridade em lote |

---

## 10) Importação/exportação CSV

| Método | Endpoint | Payload/Parâmetros | Descrição |
| --- | --- | --- | --- |
| GET | `/kanban_items/export` | `funnel_id` + filtros opcionais | Exporta CSV |
| POST | `/kanban_items/import_preview` | multipart `file` | Pré-visualiza CSV |
| POST | `/kanban_items/import` | multipart `file`, `funnel_id`, `mappings`, opcional `default_stage_id` | Importa CSV |

---

## 11) Configuração de Kanban

| Método | Endpoint | Payload | Descrição |
| --- | --- | --- | --- |
| GET | `/kanban_config` | - | Obtém configuração |
| POST | `/kanban_config` | body `kanban_config` | Cria configuração |
| PUT/PATCH | `/kanban_config` | body `kanban_config` | Atualiza configuração |
| DELETE | `/kanban_config` | - | Exclui configuração |
| POST | `/kanban_config/test_webhook` | - | Testa webhook |

### Payload de configuração

```json
{
  "kanban_config": {
    "enabled": true,
    "webhook_url": "https://hooks.example.com/kanban",
    "webhook_secret": "secret",
    "webhook_events": ["kanban.item.created", "kanban.item.updated"],
    "config": {
      "title": "Meu Kanban",
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

## 12) Automações Kanban

### 12.1 Escopo de conta (recomendado)

| Método | Endpoint | Payload | Descrição |
| --- | --- | --- | --- |
| GET | `/kanban/automations` | - | Lista automações |
| GET | `/kanban/automations/:id` | - | Exibe automação |
| POST | `/kanban/automations` | body `kanban_automation` | Cria automação |
| PATCH/PUT | `/kanban/automations/:id` | body `kanban_automation` | Atualiza automação |
| DELETE | `/kanban/automations/:id` | - | Exclui automação |

### 12.2 Global legado (sem escopo de conta)

| Método | Endpoint | Payload | Descrição |
| --- | --- | --- | --- |
| GET | `/api/v1/kanban_automations` | - | Lista global legado |
| GET | `/api/v1/kanban_automations/:id` | - | Detalhe global legado |
| POST | `/api/v1/kanban_automations` | body `kanban_automation` | Cria registro legado |
| PATCH/PUT | `/api/v1/kanban_automations/:id` | body `kanban_automation` | Atualiza registro legado |
| DELETE | `/api/v1/kanban_automations/:id` | - | Exclui registro legado |

### 12.3 Namespace Kanban adicional

| Método | Endpoint | Payload/Parâmetros | Descrição |
| --- | --- | --- | --- |
| GET | `/kanban/funnels` | - | Lista funis via namespace Kanban |
| GET | `/kanban/funnels/:id` | `id` | Exibe funil via namespace Kanban |
| POST | `/kanban/funnels` | body `funnel` | Cria funil via namespace Kanban |
| PATCH/PUT | `/kanban/funnels/:id` | body `funnel` | Atualiza funil via namespace Kanban |
| DELETE | `/kanban/funnels/:id` | `id` | Exclui funil via namespace Kanban |
| GET | `/kanban/stages` | `funnel_id` | Lista etapas do funil |
| GET | `/kanban/stages/:id` | opcional `funnel_id` | Exibe etapa por id |
| POST | `/kanban/stages` | `funnel_id`, body `stage` | Cria etapa |
| PATCH/PUT | `/kanban/stages/:id` | opcional `funnel_id`, body `stage` | Atualiza etapa |
| DELETE | `/kanban/stages/:id` | opcional `funnel_id`, opcional `fallback_stage_id` | Exclui etapa e move itens |

---

## 13) Códigos de resposta esperados

- `200 OK`: leitura/atualização com sucesso
- `201 Created`: criação com sucesso
- `204 No Content`: exclusão sem corpo
- `400 Bad Request`: payload/parâmetros inválidos
- `401 Unauthorized`: token ausente/inválido
- `403 Forbidden`: sem permissão/licença
- `404 Not Found`: recurso não encontrado
- `422 Unprocessable Entity`: validações de negócio
- `500 Internal Server Error`: erro inesperado
