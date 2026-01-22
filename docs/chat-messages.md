# Chat Messages Endpoints

Send and manage messages in chats (group chats and task chats).

## Get Message History

Get message history for a chat.

**Endpoint:** `GET /api-v2/chats/{chatId}/messages`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `chatId` | string | Yes | Chat ID (group chat ID or task ID) |

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `limit` | number | No | 50 | Number of items (max 1000) |
| `offset` | number | No | 0 | Index of first item |
| `fromUserId` | string | No | - | Filter by sender user ID |
| `text` | string | No | - | Filter by text content |
| `label` | string | No | - | Filter by message quick link |
| `since` | number | No | - | Messages created after this timestamp |
| `includeSystem` | boolean | No | false | Include system messages |
| `includeDeleted` | boolean | No | false | Include deleted messages |

### Response

```json
{
  "paging": {
    "count": 25,
    "limit": 50,
    "offset": 0,
    "next": false
  },
  "content": [
    {
      "id": 12345,
      "text": "Hello team!",
      "fromUserId": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
      "timestamp": 1653029146646,
      "deleted": false
    }
  ]
}
```

### Example

```bash
curl -X GET "https://yougile.com/api-v2/chats/CHAT_ID/messages" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

```bash
# Get recent messages (since timestamp)
curl -X GET "https://yougile.com/api-v2/chats/CHAT_ID/messages?since=1653029146646" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

```bash
# Search messages containing text
curl -X GET "https://yougile.com/api-v2/chats/CHAT_ID/messages?text=important" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Get Message by ID

Get a specific message.

**Endpoint:** `GET /api-v2/chats/{chatId}/messages/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `chatId` | string | Yes | Chat ID |
| `id` | number | Yes | Message ID |

### Response

```json
{
  "id": 12345,
  "text": "Hello team!",
  "fromUserId": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
  "timestamp": 1653029146646,
  "deleted": false
}
```

### Example

```bash
curl -X GET "https://yougile.com/api-v2/chats/CHAT_ID/messages/12345" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Send Message

Send a message to a chat.

**Endpoint:** `POST /api-v2/chats/{chatId}/messages`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `chatId` | string | Yes | Chat ID (group chat ID or task ID) |

### Request Body

```json
{
  "text": "Hello team! Here's an update on the project."
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `text` | string | Yes | Message text (supports markdown) |

### Markdown Support

Messages support markdown formatting:
- `**bold**` - Bold text
- `*italic*` - Italic text
- `` `code` `` - Inline code
- `[link](url)` - Links
- Lists and other markdown features

### Response

```json
{
  "chatId": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X POST "https://yougile.com/api-v2/chats/CHAT_ID/messages" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"text": "Hello team!"}'
```

### Sending to Task Chat

To send a message to a task's chat, use the task ID as the `chatId`:

```bash
curl -X POST "https://yougile.com/api-v2/chats/TASK_ID/messages" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"text": "Updated the task status."}'
```

---

## Update Message

Update (edit) a message.

**Endpoint:** `PUT /api-v2/chats/{chatId}/messages/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `chatId` | string | Yes | Chat ID |
| `id` | number | Yes | Message ID |

### Request Body

```json
{
  "text": "Updated message text"
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `text` | string | No | Updated message text |

### Response

```json
{
  "chatId": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X PUT "https://yougile.com/api-v2/chats/CHAT_ID/messages/12345" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"text": "Corrected message text"}'
```
