# Group Chats Endpoints

Group chats allow team communication within Yougile.

## Get Group Chats List

Get a list of group chats.

**Endpoint:** `GET /api-v2/group-chats`

**Authentication:** Bearer token required

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `limit` | number | No | 50 | Number of items (max 1000) |
| `offset` | number | No | 0 | Index of first item |
| `title` | string | No | - | Filter by chat name |
| `includeDeleted` | boolean | No | false | Include deleted chats |

### Response

```json
{
  "paging": {
    "count": 5,
    "limit": 50,
    "offset": 0,
    "next": false
  },
  "content": [
    {
      "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
      "title": "Development Team",
      "deleted": false
    }
  ]
}
```

### Example

```bash
curl -X GET "https://yougile.com/api-v2/group-chats" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Get Group Chat by ID

Get details of a specific group chat.

**Endpoint:** `GET /api-v2/group-chats/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Chat ID |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
  "title": "Development Team",
  "deleted": false
}
```

### Example

```bash
curl -X GET "https://yougile.com/api-v2/group-chats/CHAT_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Create Group Chat

Create a new group chat.

**Endpoint:** `POST /api-v2/group-chats`

**Authentication:** Bearer token required

### Request Body

```json
{
  "title": "New Team Chat"
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `title` | string | Yes | Chat name |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X POST "https://yougile.com/api-v2/group-chats" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"title": "Project Discussion"}'
```

---

## Update Group Chat

Update group chat details.

**Endpoint:** `PUT /api-v2/group-chats/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Chat ID |

### Request Body

```json
{
  "title": "Updated Chat Name"
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `title` | string | No | Chat name |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X PUT "https://yougile.com/api-v2/group-chats/CHAT_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"title": "Renamed Chat"}'
```
