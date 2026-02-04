# Scheduled Messages API Reference

This documentation provides usage examples for the Scheduled Messages API using curl.

## Authentication

All requests require API token authentication. You must include the `api_access_token` header in each request.

```bash
# Set up environment variables
export API_TOKEN="your_api_token"
export ACCOUNT_ID="1"
export BASE_URL="http://localhost:3000"
```

---

## Scheduled Messages (Account Level)

### 1. List Scheduled Messages

Lists all scheduled messages for the account, ordered by scheduled date descending.

**Endpoint:** `GET /api/v1/accounts/:account_id/scheduled_messages`

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Example response:**

```json
{
  "payload": [
    {
      "id": 1,
      "content": "Reminder: Meeting tomorrow at 10 AM",
      "scheduled_at": 1738836000,
      "sent_at": null,
      "title": "Meeting reminder",
      "inbox_id": 5,
      "inbox_name": "WhatsApp Business",
      "conversation_id": 123,
      "contact_id": 456,
      "contact_name": "John Doe",
      "contact_phone": "+1234567890",
      "contact_email": "john@example.com",
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
      "assignee_name": "Mary Smith",
      "assignee_avatar_url": "https://example.com/avatar.png"
    }
  ]
}
```

**Possible statuses:**

- `pending`: Message waiting to be sent
- `sent`: Message sent successfully
- `failed`: Send failed

---

### 2. Show Scheduled Message

Gets the details of a specific scheduled message.

**Endpoint:** `GET /api/v1/accounts/:account_id/scheduled_messages/:id`

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages/1" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Response:** Same structure as a list item.

---

### 3. Create Scheduled Message

Creates a new scheduled message at the account level.

**Endpoint:** `POST /api/v1/accounts/:account_id/scheduled_messages`

#### 3.1 Simple Message

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Hello, this is a scheduled message",
    "scheduled_at": "2026-02-06T15:00:00Z",
    "title": "Customer follow-up"
  }'
```

#### 3.2 Message with Attachments

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -F "inbox_id=5" \
  -F "contact_id=456" \
  -F "content=Attached is the requested document" \
  -F "scheduled_at=2026-02-06T15:00:00Z" \
  -F "title=Document delivery" \
  -F "attachments[]=@/path/to/document.pdf" \
  -F "attachments[]=@/path/to/image.jpg"
```

**Limit:** Maximum 15 attachments per message.

#### 3.3 Message with WhatsApp Template

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Confirmation template",
    "scheduled_at": "2026-02-06T15:00:00Z",
    "title": "Confirm appointment",
    "template_params": {
      "name": "appointment_reminder",
      "category": "UTILITY",
      "language": "en",
      "namespace": "your_namespace",
      "processed_params": {
        "header": {},
        "body": [
          {"type": "text", "text": "John Doe"},
          {"type": "text", "text": "10:00 AM"},
          {"type": "text", "text": "February 6th"}
        ],
        "buttons": []
      }
    }
  }'
```

#### 3.4 Recurring Message

```bash
# Daily message repeating 10 times
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Daily reminder",
    "scheduled_at": "2026-02-06T09:00:00Z",
    "title": "Morning reminder",
    "recurrence_type": "daily",
    "recurrence_interval": 1,
    "recurrence_end_type": "after_occurrences",
    "recurrence_max_occurrences": 10
  }'
```

```bash
# Weekly message repeating until a date
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Weekly report",
    "scheduled_at": "2026-02-10T10:00:00Z",
    "title": "Executive report",
    "recurrence_type": "weekly",
    "recurrence_interval": 1,
    "recurrence_days": [1],
    "recurrence_end_type": "on_date",
    "recurrence_end_date": "2026-12-31"
  }'
```

```bash
# Infinite monthly message
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Monthly reminder",
    "scheduled_at": "2026-03-01T12:00:00Z",
    "title": "Monthly follow-up",
    "recurrence_type": "monthly",
    "recurrence_interval": 1,
    "recurrence_end_type": "never"
  }'
```

**Recurrence parameters:**

- `recurrence_type`: `none` (default), `daily`, `weekly`, `monthly`, `yearly`
- `recurrence_interval`: Repetition interval (e.g., 2 = every 2 days/weeks/months)
- `recurrence_days`: Array of weekdays (0=Sunday, 6=Saturday) - Only for `weekly`
- `recurrence_end_type`: `never`, `on_date`, `after_occurrences`
- `recurrence_end_date`: Date until which to repeat (ISO 8601) - Required if `recurrence_end_type` is `on_date`
- `recurrence_max_occurrences`: Maximum number of occurrences - Required if `recurrence_end_type` is `after_occurrences`

**Example response:**

```json
{
  "id": 2,
  "content": "Hello, this is a scheduled message",
  "scheduled_at": 1738854000,
  "sent_at": null,
  "title": "Customer follow-up",
  "inbox_id": 5,
  "inbox_name": "WhatsApp Business",
  "conversation_id": null,
  "contact_id": 456,
  "contact_name": "John Doe",
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

### 4. Update Scheduled Message

Updates an existing scheduled message. Only messages with `pending` status can be updated.

**Endpoint:** `PUT /api/v1/accounts/:account_id/scheduled_messages/:id`

```bash
curl -X PUT \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages/1" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "content": "Updated message",
    "scheduled_at": "2026-02-07T16:00:00Z",
    "title": "Updated title"
  }'
```

**Note:** The `status` field cannot be modified manually. It updates automatically when the message is sent or fails.

---

### 5. Delete Scheduled Message

Deletes a scheduled message. Can be deleted in any status.

**Endpoint:** `DELETE /api/v1/accounts/:account_id/scheduled_messages/:id`

```bash
curl -X DELETE \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages/1" \
  -H "api_access_token: $API_TOKEN"
```

**Response:** `204 No Content`

---

## Scheduled Messages by Conversation

### 1. List Messages for a Conversation

Lists all scheduled messages associated with a specific contact (includes all their conversations).

**Endpoint:** `GET /api/v1/accounts/:account_id/conversations/:conversation_id/scheduled_messages`

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Example response:**

```json
{
  "payload": [
    {
      "id": 1,
      "content": "Scheduled follow-up",
      "scheduled_at": 1738836000,
      "sent_at": null,
      "title": "Follow-up",
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

### 2. Show Scheduled Message

Gets the details of a specific scheduled message.

**Endpoint:** `GET /api/v1/accounts/:account_id/conversations/:conversation_id/scheduled_messages/:id`

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages/1" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

---

### 3. Create Scheduled Message in Conversation

Creates a scheduled message within an existing conversation.

**Endpoint:** `POST /api/v1/accounts/:account_id/conversations/:conversation_id/scheduled_messages`

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "scheduled_message": {
      "content": "This is a scheduled message from the conversation",
      "scheduled_at": "2026-02-06T15:00:00Z",
      "title": "Automatic follow-up",
      "inbox_id": 5
    }
  }'
```

**With attachments:**

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -F "scheduled_message[content]=Message with file" \
  -F "scheduled_message[scheduled_at]=2026-02-06T15:00:00Z" \
  -F "scheduled_message[title]=Document delivery" \
  -F "scheduled_message[inbox_id]=5" \
  -F "scheduled_message[attachments][]=@/path/to/file.pdf"
```

---

### 4. Update Scheduled Message

Updates a scheduled message in a conversation.

**Endpoint:** `PUT /api/v1/accounts/:account_id/conversations/:conversation_id/scheduled_messages/:id`

```bash
curl -X PUT \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages/1" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "scheduled_message": {
      "content": "Message updated from conversation",
      "scheduled_at": "2026-02-07T16:00:00Z"
    }
  }'
```

---

### 5. Delete Scheduled Message

Deletes a scheduled message from a conversation.

**Endpoint:** `DELETE /api/v1/accounts/:account_id/conversations/:conversation_id/scheduled_messages/:id`

```bash
curl -X DELETE \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages/1" \
  -H "api_access_token: $API_TOKEN"
```

**Response:** `200 OK`

---

### 6. Count Scheduled Messages

Counts the scheduled messages for a conversation, with option to filter by status.

**Endpoint:** `GET /api/v1/accounts/:account_id/conversations/:conversation_id/scheduled_messages/count`

```bash
# Count all messages
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages/count" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"

# Count pending messages
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/conversations/123/scheduled_messages/count?status=pending" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Response:**

```json
{
  "count": 5
}
```

---

## Common Use Cases

### 1. Automated Post-Sale Follow-up

```bash
# Schedule follow-up message 24 hours later
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Hi, how was your experience with our product?",
    "scheduled_at": "2026-02-07T10:00:00Z",
    "title": "Post-sale follow-up"
  }'
```

### 2. Appointment Reminders

```bash
# Reminder 1 day before
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Reminder: You have an appointment tomorrow at 3:00 PM",
    "scheduled_at": "2026-02-09T09:00:00Z",
    "title": "Appointment reminder"
  }'
```

### 3. Weekly Newsletters

```bash
# Newsletter every Monday at 9 AM
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 456,
    "content": "Good morning! Here is your weekly newsletter",
    "scheduled_at": "2026-02-10T09:00:00Z",
    "title": "Weekly Newsletter",
    "recurrence_type": "weekly",
    "recurrence_interval": 1,
    "recurrence_days": [1],
    "recurrence_end_type": "never"
  }'
```

### 4. Lead Nurturing Campaign

```bash
# Message 1: Immediate
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 789,
    "content": "Thank you for your interest! Here is more information...",
    "scheduled_at": "2026-02-06T10:00:00Z",
    "title": "Campaign - Day 0"
  }'

# Message 2: 3 days later
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 789,
    "content": "Have you had a chance to review the information?",
    "scheduled_at": "2026-02-09T10:00:00Z",
    "title": "Campaign - Day 3"
  }'

# Message 3: 7 days later
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/scheduled_messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "inbox_id": 5,
    "contact_id": 789,
    "content": "Special offer available for a limited time only",
    "scheduled_at": "2026-02-13T10:00:00Z",
    "title": "Campaign - Day 7"
  }'
```

---

## Permissions

### Standard Edition (OSS)

Permissions are controlled by the `ScheduledMessagePolicy`:

- **Administrators**: Full access
- **Agents**: Can manage their own scheduled messages
- **Inbox supervisor**: Can manage messages from the supervised inbox

### Enterprise Edition

In Enterprise Edition, you can assign granular permission:

- `scheduled_message_manage`: Allows managing all scheduled messages in the account

This permission can be assigned to Custom Roles.

---

## Important Notes

1. **Timezone**: All dates must be sent in ISO 8601 format (UTC). The system will convert them according to the account's timezone.

2. **Date Validation**: Cannot schedule a message in the past.

3. **Attachment Limit**: Maximum 15 files per message.

4. **Statuses**:
   - Messages are created with `pending` status
   - Change to `sent` when sent successfully
   - Change to `failed` if there's an error sending

5. **Asynchronous Job**: Messages are sent via `ScheduledMessageJob` which executes at the scheduled date/time.

6. **Recurrence**:
   - Recurring messages automatically create the next occurrence after being sent
   - Recurrence can be stopped by deleting the parent message
   - The `parent_id` field indicates if it's an occurrence of a recurring message

7. **WhatsApp Templates**:
   - Templates must be previously approved in WhatsApp Business API
   - Parameters must exactly match the template structure

8. **Deletion**:
   - Deleting a `pending` message cancels its sending
   - Deleting a recurring parent message stops all future occurrences

---

## Common Error Codes

- `404 Not Found`: The scheduled message doesn't exist or doesn't belong to the account
- `422 Unprocessable Entity`: Validation errors (invalid date, required fields, etc.)
- `403 Forbidden`: No permissions to perform the action

**Error examples:**

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

The system emits the following events for scheduled messages:

- `scheduled_message.created`: When a scheduled message is created
- `scheduled_message.updated`: When a scheduled message is updated
- `scheduled_message.deleted`: When a scheduled message is deleted

These events can be captured via webhooks configured in the account.

---