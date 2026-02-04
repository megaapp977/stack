# Chat Rooms API Reference

This documentation provides usage examples for the Chat Rooms API using curl.

## Authentication

All requests require API token authentication. You must include the `api_access_token` header in each request.

```bash
# Set up environment variables
export API_TOKEN="your_api_token"
export ACCOUNT_ID="1"
export BASE_URL="http://localhost:3000"
```

---

## Chat Rooms

### 1. List Chat Rooms

Lists all chat rooms for the account.

**Endpoint:** `GET /api/v1/accounts/:account_id/chat_rooms`

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Example response:**
```json
[
  {
    "id": 1,
    "name": "Development Team",
    "description": "Room for the development team",
    "account_id": 1,
    "avatar_url": "https://example.com/avatar.png",
    "is_member": true,
    "member_count": 5,
    "last_message_at": 1640000000,
    "unread_count": 3,
    "members": [
      {
        "id": 1,
        "name": "John Doe",
        "email": "john@example.com",
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

### 2. Create Chat Room

Creates a new chat room.

**Endpoint:** `POST /api/v1/accounts/:account_id/chat_rooms`

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "chat_room": {
      "name": "Marketing Team",
      "description": "Room to coordinate marketing campaigns"
    }
  }'
```

**With avatar (file):**
```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms" \
  -H "api_access_token: $API_TOKEN" \
  -F "chat_room[name]=Marketing Team" \
  -F "chat_room[description]=Room to coordinate campaigns" \
  -F "chat_room[avatar]=@/path/to/avatar.png"
```

**Example response:**
```json
{
  "id": 2,
  "name": "Marketing Team",
  "description": "Room to coordinate marketing campaigns",
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

### 3. Get Chat Room

Gets details of a specific chat room.

**Endpoint:** `GET /api/v1/accounts/:account_id/chat_rooms/:id`

```bash
export CHAT_ROOM_ID="1"

curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Example response:**
```json
{
  "id": 1,
  "name": "Development Team",
  "description": "Room for the development team",
  "account_id": 1,
  "avatar_url": "https://example.com/avatar.png",
  "is_member": true,
  "member_count": 5,
  "last_message_at": 1640000000,
  "unread_count": 3,
  "members": [
    {
      "id": 1,
      "name": "John Doe",
      "email": "john@example.com",
      "thumbnail": "https://example.com/avatar1.png",
      "availability_status": "online"
    }
  ],
  "created_at": 1640000000,
  "updated_at": 1640000000
}
```

---

### 4. Update Chat Room

Updates the details of a chat room.

**Endpoint:** `PUT /api/v1/accounts/:account_id/chat_rooms/:id`

```bash
curl -X PUT \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "chat_room": {
      "name": "Development Team - Updated",
      "description": "New description for the team"
    }
  }'
```

**Update with avatar:**
```bash
curl -X PUT \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID" \
  -H "api_access_token: $API_TOKEN" \
  -F "chat_room[name]=Development Team - Updated" \
  -F "chat_room[avatar]=@/path/to/new_avatar.png"
```

**Example response:**
```json
{
  "id": 1,
  "name": "Development Team - Updated",
  "description": "New description for the team",
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

### 5. Delete Chat Room

Deletes a chat room.

**Endpoint:** `DELETE /api/v1/accounts/:account_id/chat_rooms/:id`

```bash
curl -X DELETE \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID" \
  -H "api_access_token: $API_TOKEN"
```

**Response:** Status `200 OK` with no content

---

### 6. Mark as Read

Marks all messages in a room as read for the current user.

**Endpoint:** `POST /api/v1/accounts/:account_id/chat_rooms/:id/mark_as_read`

```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/mark_as_read" \
  -H "api_access_token: $API_TOKEN"
```

**Response:** Status `200 OK` with no content

---

## Chat Room Members

### 7. List Members

Lists all members of a chat room.

**Endpoint:** `GET /api/v1/accounts/:account_id/chat_rooms/:chat_room_id/members`

```bash
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/members" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Example response:**
```json
[
  {
    "id": 1,
    "name": "John Doe",
    "email": "john@example.com",
    "account_id": 1,
    "role": "agent",
    "confirmed": true,
    "availability_status": "online",
    "thumbnail": "https://example.com/avatar1.png"
  },
  {
    "id": 2,
    "name": "Jane Smith",
    "email": "jane@example.com",
    "account_id": 1,
    "role": "agent",
    "confirmed": true,
    "availability_status": "offline",
    "thumbnail": "https://example.com/avatar2.png"
  }
]
```

---

### 8. Add Members

Adds one or more members to a chat room.

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

**Example response:**
```json
[
  {
    "id": 3,
    "name": "Peter Johnson",
    "email": "peter@example.com",
    "account_id": 1,
    "role": "agent",
    "confirmed": true,
    "availability_status": "online",
    "thumbnail": "https://example.com/avatar3.png"
  },
  {
    "id": 4,
    "name": "Anna Williams",
    "email": "anna@example.com",
    "account_id": 1,
    "role": "agent",
    "confirmed": true,
    "availability_status": "busy",
    "thumbnail": "https://example.com/avatar4.png"
  }
]
```

---

### 9. Update Members

Updates the complete list of members in a room (adds and/or removes members).

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

> **Note:** This operation sets the complete member list. Users not included in `user_ids` will be removed, and new ones will be added.

**Example response:**
```json
[
  {
    "id": 1,
    "name": "John Doe",
    "email": "john@example.com",
    "account_id": 1,
    "role": "agent",
    "confirmed": true,
    "availability_status": "online",
    "thumbnail": "https://example.com/avatar1.png"
  },
  {
    "id": 2,
    "name": "Jane Smith",
    "email": "jane@example.com",
    "account_id": 1,
    "role": "agent",
    "confirmed": true,
    "availability_status": "offline",
    "thumbnail": "https://example.com/avatar2.png"
  },
  {
    "id": 3,
    "name": "Peter Johnson",
    "email": "peter@example.com",
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

### 10. Remove Members

Removes one or more members from a chat room.

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

**Response:** Status `200 OK` with no content

---

## Chat Room Messages

### 11. List Messages

Lists messages from a chat room with pagination.

**Endpoint:** `GET /api/v1/accounts/:account_id/chat_rooms/:chat_room_id/messages`

```bash
# List messages (page 1)
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**With pagination:**
```bash
# Page 2, 50 messages per page
curl -X GET \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/messages?page=2&per_page=50" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json"
```

**Response headers with pagination information:**
```
X-Total-Count: 150
X-Current-Page: 1
X-Per-Page: 20
X-Total-Pages: 8
```

**Example response:**
```json
[
  {
    "id": 1,
    "content": "Hi team, how's the project going?",
    "message_type": "outgoing",
    "content_type": "text",
    "content_attributes": {},
    "created_at": 1640000000,
    "conversation_id": 1,
    "room_name": "Development Team",
    "sender": {
      "id": 1,
      "name": "John Doe",
      "email": "john@example.com",
      "thumbnail": "https://example.com/avatar1.png",
      "availability_status": "online"
    },
    "attachments": [],
    "status": "sent"
  },
  {
    "id": 2,
    "content": "All good, we're progressing as planned",
    "message_type": "incoming",
    "content_type": "text",
    "content_attributes": {
      "in_reply_to": 1
    },
    "created_at": 1640000060,
    "conversation_id": 1,
    "room_name": "Development Team",
    "sender": {
      "id": 2,
      "name": "Jane Smith",
      "email": "jane@example.com",
      "thumbnail": "https://example.com/avatar2.png",
      "availability_status": "online"
    },
    "attachments": [],
    "status": "read",
    "in_reply_to": {
      "id": 1,
      "content": "Hi team, how's the project going?",
      "sender": {
        "id": 1,
        "name": "John Doe"
      }
    }
  }
]
```

---

### 12. Send Message

Sends a new message to a chat room.

**Endpoint:** `POST /api/v1/accounts/:account_id/chat_rooms/:chat_room_id/messages`

**Simple text message:**
```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "chat_room_message": {
      "content": "This is a test message",
      "message_type": "outgoing"
    }
  }'
```

**Message with echo_id (for synchronization):**
```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "chat_room_message": {
      "content": "Message with temporary identifier",
      "message_type": "outgoing",
      "echo_id": "temp-msg-12345"
    }
  }'
```

**Reply to another message:**
```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/messages" \
  -H "api_access_token: $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "chat_room_message": {
      "content": "Replying to the previous message",
      "message_type": "outgoing",
      "content_attributes": {
        "in_reply_to": 123
      }
    }
  }'
```

**Message with file attachments:**
```bash
curl -X POST \
  "$BASE_URL/api/v1/accounts/$ACCOUNT_ID/chat_rooms/$CHAT_ROOM_ID/messages" \
  -H "api_access_token: $API_TOKEN" \
  -F "chat_room_message[content]=Attaching some files" \
  -F "chat_room_message[message_type]=outgoing" \
  -F "chat_room_message[attachments][]=@/path/to/document.pdf" \
  -F "chat_room_message[attachments][]=@/path/to/image.png"
```

**Example response:**
```json
{
  "id": 150,
  "content": "This is a test message",
  "message_type": "outgoing",
  "content_type": "text",
  "content_attributes": {},
  "created_at": 1640000500,
  "conversation_id": 1,
  "room_name": "Development Team",
  "sender": {
    "id": 1,
    "name": "John Doe",
    "email": "john@example.com",
    "thumbnail": "https://example.com/avatar1.png",
    "availability_status": "online"
  },
  "attachments": [],
  "status": "sent"
}
```

---

## Error Codes

### Common errors:

- **401 Unauthorized**: Invalid or missing API token
- **403 Forbidden**: 
  - Chat rooms feature is not enabled for the account
  - User is not a member of the chat room
  - Insufficient permissions
- **404 Not Found**: Resource not found (room, message, user)
- **422 Unprocessable Entity**: Validation errors

**Error example:**
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

## Additional Notes

### Message Pagination

- Default: 20 messages per page
- Maximum: 50 messages per page
- Messages are returned from newest to oldest
- Use response headers for pagination information

### Message Status

- `sent`: Message sent
- `delivered`: Message delivered (all members have been notified)
- `read`: Message read by all members (except the sender)

### Attachments

- Supports multiple files per message
- Use `multipart/form-data` to send files
- Files can be images, documents, videos, etc.

### Message Replies

- Use `content_attributes.in_reply_to` with the original message ID
- The API returns the original message data in the `in_reply_to` field

### Permissions

- Only room members can view and send messages
- Only administrators can view all rooms (list)
- Regular users only see rooms they are members of
- Only administrators can create/update/delete rooms
