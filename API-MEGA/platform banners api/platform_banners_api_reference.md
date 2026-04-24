# Platform Banners API Reference

## Overview

Platform Banners allow Super Admins to display important messages, alerts, and announcements to users across the platform. Banners support markdown formatting for rich text content.

## Features

- **Rich Text Content**: Support for markdown (`**bold**`, `*italic*`, `[link](url)`)
- **Banner Types**: info, warning, error, success (with corresponding colors and icons)
- **Scheduling**: Set start and end dates for time-limited banners
- **Targeting**: Show banners to specific accounts or user roles
- **Dismiss Persistence**: Users can dismiss banners, and this is saved per-user
- **Real-time Updates**: Banners broadcast changes via ActionCable

---

## Platform API (for external integrations)

Base URL: `/platform/api/v1/platform_banners`

**Authentication**: Requires `api_access_token` header with a valid PlatformApp token.

### List All Banners

```http
GET /platform/api/v1/platform_banners
```

**Headers:**

```
api_access_token: YOUR_PLATFORM_APP_TOKEN
```

**Response (200 OK):**

```json
[
  {
    "id": 1,
    "title": "Scheduled Maintenance",
    "content": "We will have **scheduled maintenance** on Friday. [Check status](https://status.example.com)",
    "formatted_content": "We will have <strong>scheduled maintenance</strong> on Friday. <a href=\"https://status.example.com\" target=\"_blank\" rel=\"noopener noreferrer\">Check status</a>",
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

### Create a Banner

```http
POST /platform/api/v1/platform_banners
```

**Headers:**

```
api_access_token: YOUR_PLATFORM_APP_TOKEN
Content-Type: application/json
```

**Request Body:**

```json
{
  "title": "Important Announcement",
  "content": "We are experiencing issues with **WhatsApp API**. [View status](https://metastatus.com)",
  "banner_type": "warning",
  "active": true,
  "starts_at": "2026-04-15T00:00:00Z",
  "ends_at": "2026-04-16T00:00:00Z",
  "target_accounts": [1, 2, 3],
  "target_user_roles": "all_users",
  "status_url": "https://status.example.com"
}
```

**Response (201 Created):**

```json
{
  "id": 2,
  "title": "Important Announcement",
  "content": "We are experiencing issues with **WhatsApp API**. [View status](https://metastatus.com)",
  "formatted_content": "We are experiencing issues with <strong>WhatsApp API</strong>. <a href=\"https://metastatus.com\" target=\"_blank\" rel=\"noopener noreferrer\">View status</a>",
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

### Get a Banner

```http
GET /platform/api/v1/platform_banners/:id
```

**Response (200 OK):** Same as single banner object above.

### Update a Banner

```http
PATCH /platform/api/v1/platform_banners/:id
```

**Request Body:** (only include fields to update)

```json
{
  "title": "Updated Title",
  "banner_type": "error",
  "active": false
}
```

**Response (200 OK):** Updated banner object.

### Delete a Banner

```http
DELETE /platform/api/v1/platform_banners/:id
```

**Response (200 OK):** Empty response.

---

## Account API (for dashboard users)

Base URL: `/api/v1/accounts/:account_id/platform_banners`

**Authentication**: Requires standard user authentication token.

### List Active Banners for User

```http
GET /api/v1/accounts/:account_id/platform_banners
```

Returns only banners that:

- Are currently active
- Match the user's account
- Match the user's role
- Haven't been dismissed by the user

**Response (200 OK):**

```json
[
  {
    "id": 1,
    "title": "System Update",
    "formatted_content": "We have <strong>new features</strong> available!",
    "banner_type": "info",
    "status_url": null,
    "created_at": "2026-04-11T00:00:00Z",
    "updated_at": "2026-04-11T00:00:00Z"
  }
]
```

### Dismiss a Banner

```http
POST /api/v1/accounts/:account_id/platform_banners/:id/dismiss
```

Dismisses a specific banner for the current user. The banner won't appear again for this user.

**Response (200 OK):** Empty response.

### Dismiss All Banners

```http
POST /api/v1/accounts/:account_id/platform_banners/dismiss_all
```

Dismisses all currently visible banners for the current user.

**Response (200 OK):** Empty response.

---

## Data Model

### Banner Fields

| Field | Type | Description |
|-------|------|-------------|
| `id` | integer | Unique identifier |
| `title` | string | Banner title (required) |
| `content` | text | Raw content with markdown support (required) |
| `formatted_content` | string | HTML-formatted content (read-only) |
| `banner_type` | enum | `info`, `warning`, `error`, `success` |
| `active` | boolean | Whether the banner is active (default: true) |
| `starts_at` | datetime | When to start showing (null = immediately) |
| `ends_at` | datetime | When to stop showing (null = indefinitely) |
| `status_url` | string | Optional additional status page URL |
| `target_accounts` | array | Account IDs to target (null = all accounts) |
| `target_user_roles` | enum | `all_users`, `admin_only` |
| `created_at` | datetime | Creation timestamp |
| `updated_at` | datetime | Last update timestamp |

### Banner Types

| Type | Color | Icon | Use Case |
|------|-------|------|----------|
| `info` | Blue | ℹ️ | General announcements, new features |
| `warning` | Yellow | ⚠️ | Upcoming maintenance, known issues |
| `error` | Red | ❌ | Critical outages, urgent problems |
| `success` | Green | ✅ | Issue resolved, positive updates |

---

## Markdown Support

The `content` field supports basic markdown formatting:

| Markdown | Result | Example |
|----------|--------|---------|
| `**text**` | **Bold** | `**Important**` → **Important** |
| `*text*` | *Italic* | `*Note*` → *Note* |
| `[text](url)` | Link | `[See here](https://example.com)` → [See here](https://example.com) |

**Example content:**

```
We are experiencing issues with the **Meta API**. Our team is working on it. [Check our status page](https://status.example.com) for updates.
```

**Renders as:**
> We are experiencing issues with the **Meta API**. Our team is working on it. [Check our status page](https://status.example.com) for updates.

---

## Usage Examples

### cURL Examples

```bash
# Set your token
TOKEN="YOUR_PLATFORM_APP_TOKEN"

# List all banners
curl -s http://localhost:3000/platform/api/v1/platform_banners \
  -H "api_access_token: $TOKEN" | jq .

# Create a maintenance banner
curl -X POST http://localhost:3000/platform/api/v1/platform_banners \
  -H "api_access_token: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Scheduled Maintenance",
    "content": "We will have maintenance on **Friday 10PM**. [Status page](https://status.example.com)",
    "banner_type": "warning",
    "starts_at": "2026-04-15T00:00:00Z",
    "ends_at": "2026-04-16T00:00:00Z"
  }'

# Create an incident banner
curl -X POST http://localhost:3000/platform/api/v1/platform_banners \
  -H "api_access_token: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "WhatsApp API Issues",
    "content": "We are experiencing problems with the WhatsApp API. **Messages may be delayed**. [Meta Status](https://metastatus.com)",
    "banner_type": "error"
  }'

# Update banner to resolved
curl -X PATCH http://localhost:3000/platform/api/v1/platform_banners/1 \
  -H "api_access_token: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "WhatsApp API Issues - RESOLVED",
    "content": "The WhatsApp API issues have been **resolved**. Thank you for your patience!",
    "banner_type": "success"
  }'

# Deactivate a banner
curl -X PATCH http://localhost:3000/platform/api/v1/platform_banners/1 \
  -H "api_access_token: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"active": false}'

# Delete a banner
curl -X DELETE http://localhost:3000/platform/api/v1/platform_banners/1 \
  -H "api_access_token: $TOKEN"
```

### JavaScript/Axios Example

```javascript
import axios from 'axios';

const api = axios.create({
  baseURL: 'https://your-instance.com/platform/api/v1',
  headers: {
    'api_access_token': 'YOUR_TOKEN'
  }
});

// Create banner
const banner = await api.post('/platform_banners', {
  title: 'New Feature Available',
  content: 'Check out our **new dashboard**! [Learn more](https://docs.example.com)',
  banner_type: 'info'
});

// Update banner
await api.patch(`/platform_banners/${banner.data.id}`, {
  banner_type: 'success'
});

// Delete banner
await api.delete(`/platform_banners/${banner.data.id}`);
```

---

## Real-time Updates

Banners are broadcast via ActionCable when created, updated, or deleted. The frontend automatically refreshes the banner list when changes are detected.

**Channel:** `PlatformBannersChannel`

---

## Super Admin Dashboard

Super Admins can also manage banners via the web interface at:

```
/super_admin/platform_banners
```

The dashboard provides:

- List of all banners with status indicators
- Create/Edit forms with markdown help
- Filtering by active status and type
- Quick activation/deactivation

---

## Configuration

Platform Banners are controlled via a DB-backed configuration toggle (`ENABLE_PLATFORM_BANNERS`), managed through `GlobalConfigService` and editable in the **Super Admin** panel under App Config → General.

When disabled:

- The Account API index endpoint returns an empty array (`[]`)
- The Account API dismiss/dismiss_all endpoints return `404`
- The Platform API endpoints return `404`
- The Super Admin sidebar hides the Platform Banners section
