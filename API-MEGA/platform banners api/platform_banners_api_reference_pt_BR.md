# Referência de API de Platform Banners

## Visão Geral

Platform Banners permite que Super Admins exibam mensagens importantes, alertas e anúncios aos usuários da plataforma. Os banners suportam formatação markdown para conteúdo rico.

## Recursos

- **Conteúdo Rico**: Suporte para markdown (`**negrito**`, `*itálico*`, `[link](url)`)
- **Tipos de Banner**: info, warning, error, success (com cores e ícones correspondentes)
- **Agendamento**: Definir datas de início e fim para banners temporários
- **Segmentação**: Mostrar banners para contas específicas ou funções de usuário
- **Persistência de Dismiss**: Usuários podem fechar banners e isso é salvo por usuário
- **Atualizações em Tempo Real**: Banners transmitem mudanças via ActionCable

---

## Platform API (para integrações externas)

URL Base: `/platform/api/v1/platform_banners`

**Autenticação**: Requer header `api_access_token` com um token válido de PlatformApp.

### Listar Todos os Banners

```http
GET /platform/api/v1/platform_banners
```

**Headers:**

```
api_access_token: SEU_TOKEN_DE_PLATFORM_APP
```

**Resposta (200 OK):**

```json
[
  {
    "id": 1,
    "title": "Manutenção Programada",
    "content": "Teremos **manutenção programada** na sexta-feira. [Ver status](https://status.example.com)",
    "formatted_content": "Teremos <strong>manutenção programada</strong> na sexta-feira. <a href=\"https://status.example.com\" target=\"_blank\" rel=\"noopener noreferrer\">Ver status</a>",
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

### Criar um Banner

```http
POST /platform/api/v1/platform_banners
```

**Headers:**

```
api_access_token: SEU_TOKEN_DE_PLATFORM_APP
Content-Type: application/json
```

**Corpo da Requisição:**

```json
{
  "title": "Anúncio Importante",
  "content": "Estamos enfrentando problemas com a **API do WhatsApp**. [Ver status](https://metastatus.com)",
  "banner_type": "warning",
  "active": true,
  "starts_at": "2026-04-15T00:00:00Z",
  "ends_at": "2026-04-16T00:00:00Z",
  "target_accounts": [1, 2, 3],
  "target_user_roles": "all_users",
  "status_url": "https://status.example.com"
}
```

**Resposta (201 Created):**

```json
{
  "id": 2,
  "title": "Anúncio Importante",
  "content": "Estamos enfrentando problemas com a **API do WhatsApp**. [Ver status](https://metastatus.com)",
  "formatted_content": "Estamos enfrentando problemas com a <strong>API do WhatsApp</strong>. <a href=\"https://metastatus.com\" target=\"_blank\" rel=\"noopener noreferrer\">Ver status</a>",
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

### Obter um Banner

```http
GET /platform/api/v1/platform_banners/:id
```

**Resposta (200 OK):** Mesmo objeto de banner individual.

### Atualizar um Banner

```http
PATCH /platform/api/v1/platform_banners/:id
```

**Corpo da Requisição:** (incluir apenas campos a atualizar)

```json
{
  "title": "Título Atualizado",
  "banner_type": "error",
  "active": false
}
```

**Resposta (200 OK):** Objeto do banner atualizado.

### Excluir um Banner

```http
DELETE /platform/api/v1/platform_banners/:id
```

**Resposta (200 OK):** Resposta vazia.

---

## Account API (para usuários do dashboard)

URL Base: `/api/v1/accounts/:account_id/platform_banners`

**Autenticação**: Requer token de autenticação de usuário padrão.

### Listar Banners Ativos para o Usuário

```http
GET /api/v1/accounts/:account_id/platform_banners
```

Retorna apenas banners que:

- Estão atualmente ativos
- Correspondem à conta do usuário
- Correspondem à função do usuário
- Não foram fechados pelo usuário

**Resposta (200 OK):**

```json
[
  {
    "id": 1,
    "title": "Atualização do Sistema",
    "formatted_content": "Temos <strong>novos recursos</strong> disponíveis!",
    "banner_type": "info",
    "status_url": null,
    "created_at": "2026-04-11T00:00:00Z",
    "updated_at": "2026-04-11T00:00:00Z"
  }
]
```

### Fechar um Banner

```http
POST /api/v1/accounts/:account_id/platform_banners/:id/dismiss
```

Fecha um banner específico para o usuário atual. O banner não aparecerá novamente para este usuário.

**Resposta (200 OK):** Resposta vazia.

### Fechar Todos os Banners

```http
POST /api/v1/accounts/:account_id/platform_banners/dismiss_all
```

Fecha todos os banners visíveis atualmente para o usuário atual.

**Resposta (200 OK):** Resposta vazia.

---

## Modelo de Dados

### Campos do Banner

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `id` | integer | Identificador único |
| `title` | string | Título do banner (obrigatório) |
| `content` | text | Conteúdo raw com suporte markdown (obrigatório) |
| `formatted_content` | string | Conteúdo formatado em HTML (somente leitura) |
| `banner_type` | enum | `info`, `warning`, `error`, `success` |
| `active` | boolean | Se o banner está ativo (padrão: true) |
| `starts_at` | datetime | Quando começar a mostrar (null = imediatamente) |
| `ends_at` | datetime | Quando parar de mostrar (null = indefinidamente) |
| `status_url` | string | URL adicional opcional de página de status |
| `target_accounts` | array | IDs de contas alvo (null = todas as contas) |
| `target_user_roles` | enum | `all_users`, `admin_only` |
| `created_at` | datetime | Data de criação |
| `updated_at` | datetime | Data da última atualização |

### Tipos de Banner

| Tipo | Cor | Ícone | Caso de Uso |
|------|-----|-------|-------------|
| `info` | Azul | ℹ️ | Anúncios gerais, novos recursos |
| `warning` | Amarelo | ⚠️ | Manutenção próxima, problemas conhecidos |
| `error` | Vermelho | ❌ | Quedas críticas, problemas urgentes |
| `success` | Verde | ✅ | Problema resolvido, atualizações positivas |

---

## Suporte a Markdown

O campo `content` suporta formatação markdown básica:

| Markdown | Resultado | Exemplo |
|----------|-----------|---------|
| `**texto**` | **Negrito** | `**Importante**` → **Importante** |
| `*texto*` | *Itálico* | `*Nota*` → *Nota* |
| `[texto](url)` | Link | `[Ver aqui](https://example.com)` → [Ver aqui](https://example.com) |

**Exemplo de conteúdo:**

```
Estamos enfrentando problemas com a **API do Meta**. Nossa equipe está trabalhando nisso. [Ver página de status](https://status.example.com) para atualizações.
```

**Renderiza como:**
> Estamos enfrentando problemas com a **API do Meta**. Nossa equipe está trabalhando nisso. [Ver página de status](https://status.example.com) para atualizações.

---

## Exemplos de Uso

### Exemplos com cURL

```bash
# Definir seu token
TOKEN="SEU_TOKEN_DE_PLATFORM_APP"

# Listar todos os banners
curl -s http://localhost:3000/platform/api/v1/platform_banners \
  -H "api_access_token: $TOKEN" | jq .

# Criar um banner de manutenção
curl -X POST http://localhost:3000/platform/api/v1/platform_banners \
  -H "api_access_token: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Manutenção Programada",
    "content": "Teremos manutenção na **sexta-feira às 22:00**. [Página de status](https://status.example.com)",
    "banner_type": "warning",
    "starts_at": "2026-04-15T00:00:00Z",
    "ends_at": "2026-04-16T00:00:00Z"
  }'

# Criar um banner de incidente
curl -X POST http://localhost:3000/platform/api/v1/platform_banners \
  -H "api_access_token: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Problemas com API do WhatsApp",
    "content": "Estamos enfrentando problemas com a API do WhatsApp. **As mensagens podem atrasar**. [Status do Meta](https://metastatus.com)",
    "banner_type": "error"
  }'

# Atualizar banner para resolvido
curl -X PATCH http://localhost:3000/platform/api/v1/platform_banners/1 \
  -H "api_access_token: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Problemas com API do WhatsApp - RESOLVIDO",
    "content": "Os problemas com a API do WhatsApp foram **resolvidos**. Obrigado pela paciência!",
    "banner_type": "success"
  }'

# Desativar um banner
curl -X PATCH http://localhost:3000/platform/api/v1/platform_banners/1 \
  -H "api_access_token: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"active": false}'

# Excluir um banner
curl -X DELETE http://localhost:3000/platform/api/v1/platform_banners/1 \
  -H "api_access_token: $TOKEN"
```

### Exemplo com JavaScript/Axios

```javascript
import axios from 'axios';

const api = axios.create({
  baseURL: 'https://sua-instancia.com/platform/api/v1',
  headers: {
    'api_access_token': 'SEU_TOKEN'
  }
});

// Criar banner
const banner = await api.post('/platform_banners', {
  title: 'Novo Recurso Disponível',
  content: 'Confira nosso **novo dashboard**! [Saiba mais](https://docs.example.com)',
  banner_type: 'info'
});

// Atualizar banner
await api.patch(`/platform_banners/${banner.data.id}`, {
  banner_type: 'success'
});

// Excluir banner
await api.delete(`/platform_banners/${banner.data.id}`);
```

---

## Atualizações em Tempo Real

Os banners são transmitidos via ActionCable quando criados, atualizados ou excluídos. O frontend atualiza automaticamente a lista de banners quando mudanças são detectadas.

**Canal:** `PlatformBannersChannel`

---

## Dashboard de Super Admin

Super Admins também podem gerenciar banners via interface web em:

```
/super_admin/platform_banners
```

O dashboard fornece:

- Lista de todos os banners com indicadores de status
- Formulários de Criar/Editar com ajuda de markdown
- Filtro por status ativo e tipo
- Ativação/desativação rápida

---

## Configuração

Os Platform Banners são controlados por um toggle de configuração armazenado em banco de dados (`ENABLE_PLATFORM_BANNERS`), gerenciado pelo `GlobalConfigService` e editável no painel de **Super Admin** em App Config → General.

Quando desabilitado:

- O endpoint index da Account API retorna um array vazio (`[]`)
- Os endpoints dismiss/dismiss_all da Account API retornam `404`
- Os endpoints da Platform API retornam `404`
- A barra lateral do Super Admin oculta a seção Platform Banners
