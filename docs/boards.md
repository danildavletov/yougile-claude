# Boards Endpoints

Boards are kanban-style boards within projects that contain columns and tasks.

## Get Boards List

Get a list of boards.

**Endpoint:** `GET /api-v2/boards`

**Authentication:** Bearer token required

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `limit` | number | No | 50 | Number of items (max 1000) |
| `offset` | number | No | 0 | Index of first item |
| `title` | string | No | - | Filter by board name |
| `projectId` | string | No | - | Filter by project ID |
| `includeDeleted` | boolean | No | false | Include deleted boards |

### Response

```json
{
  "paging": {
    "count": 3,
    "limit": 50,
    "offset": 0,
    "next": false
  },
  "content": [
    {
      "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
      "title": "Development Board",
      "projectId": "001623dc-6501-461b-9de6-c1d1d6fc1d16",
      "deleted": false,
      "stickers": {
        "timer": false,
        "deadline": true,
        "stopwatch": true,
        "timeTracking": true,
        "assignee": true,
        "repeat": false,
        "custom": {
          "fbc30a9b-42d0-4cf7-80c0-31fb048346f9": true,
          "645250ca-1ae8-4514-914d-c070351dd905": true
        }
      }
    }
  ]
}
```

### Stickers Configuration

The `stickers` object defines which stickers are enabled on the board:
- `timer` - Timer sticker
- `deadline` - Deadline sticker
- `stopwatch` - Stopwatch sticker
- `timeTracking` - Time tracking sticker
- `assignee` - Assignee sticker
- `repeat` - Recurring task sticker
- `custom` - Map of custom sticker IDs to enabled status

### Example

```bash
curl -X GET "https://yougile.com/api-v2/boards" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

```bash
# Filter by project
curl -X GET "https://yougile.com/api-v2/boards?projectId=PROJECT_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Get Board by ID

Get details of a specific board.

**Endpoint:** `GET /api-v2/boards/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Board ID |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
  "title": "Development Board",
  "projectId": "001623dc-6501-461b-9de6-c1d1d6fc1d16",
  "deleted": false,
  "stickers": {
    "deadline": true,
    "assignee": true
  }
}
```

### Example

```bash
curl -X GET "https://yougile.com/api-v2/boards/4f6f0391-0f94-4d30-9b0e-99430a36d4fb" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Create Board

Create a new board in a project.

**Endpoint:** `POST /api-v2/boards`

**Authentication:** Bearer token required

### Request Body

```json
{
  "title": "New Board",
  "projectId": "001623dc-6501-461b-9de6-c1d1d6fc1d16",
  "stickers": {
    "deadline": true,
    "assignee": true,
    "timeTracking": false
  }
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `title` | string | Yes | Board name |
| `projectId` | string | Yes | ID of the project to create board in |
| `stickers` | object | No | Sticker configuration |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X POST "https://yougile.com/api-v2/boards" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Sprint Board",
    "projectId": "001623dc-6501-461b-9de6-c1d1d6fc1d16"
  }'
```

---

## Update Board

Update board details.

**Endpoint:** `PUT /api-v2/boards/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Board ID |

### Request Body

```json
{
  "title": "Updated Board Name",
  "projectId": "new-project-id",
  "stickers": {
    "deadline": true,
    "timer": true
  },
  "deleted": false
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `title` | string | No | Board name |
| `projectId` | string | No | Project ID (to move board) |
| `stickers` | object | No | Sticker configuration |
| `deleted` | boolean | No | Set to true to delete |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X PUT "https://yougile.com/api-v2/boards/4f6f0391-0f94-4d30-9b0e-99430a36d4fb" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"title": "Renamed Board"}'
```
