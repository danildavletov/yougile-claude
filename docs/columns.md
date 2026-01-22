# Columns Endpoints

Columns are vertical sections within boards that contain tasks.

## Get Columns List

Get a list of columns.

**Endpoint:** `GET /api-v2/columns`

**Authentication:** Bearer token required

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `limit` | number | No | 50 | Number of items (max 1000) |
| `offset` | number | No | 0 | Index of first item |
| `title` | string | No | - | Filter by column name |
| `boardId` | string | No | - | Filter by board ID |
| `includeDeleted` | boolean | No | false | Include deleted columns |

### Response

```json
{
  "paging": {
    "count": 4,
    "limit": 50,
    "offset": 0,
    "next": false
  },
  "content": [
    {
      "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
      "title": "To Do",
      "boardId": "0d923a9f-3675-43c6-84ce-f3580cf5e760",
      "color": 1,
      "deleted": false
    }
  ]
}
```

### Column Colors

Colors are specified as numbers 1-16:

| Number | Color Code | Description |
|--------|------------|-------------|
| 1 | #7B869E | Gray |
| 2 | #FF8C8C | Light Red |
| 3 | #E9A24F | Orange |
| 4 | #FCE258 | Yellow |
| 5 | #7CAE5E | Green |
| 6 | #49C5BC | Teal |
| 7 | #8CACFF | Light Blue |
| 8 | #CC8CFF | Light Purple |
| 9 | #667085 | Dark Gray |
| 10 | #EB3737 | Red |
| 11 | #F2732B | Dark Orange |
| 12 | #F5CC00 | Gold |
| 13 | #5CDC11 | Lime |
| 14 | #08A7A9 | Cyan |
| 15 | #5089F2 | Blue |
| 16 | #E25EF2 | Purple |

### Example

```bash
curl -X GET "https://yougile.com/api-v2/columns" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

```bash
# Filter by board
curl -X GET "https://yougile.com/api-v2/columns?boardId=BOARD_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Get Column by ID

Get details of a specific column.

**Endpoint:** `GET /api-v2/columns/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Column ID |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
  "title": "To Do",
  "boardId": "0d923a9f-3675-43c6-84ce-f3580cf5e760",
  "color": 1,
  "deleted": false
}
```

### Example

```bash
curl -X GET "https://yougile.com/api-v2/columns/4f6f0391-0f94-4d30-9b0e-99430a36d4fb" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Create Column

Create a new column in a board.

**Endpoint:** `POST /api-v2/columns`

**Authentication:** Bearer token required

### Request Body

```json
{
  "title": "In Progress",
  "boardId": "0d923a9f-3675-43c6-84ce-f3580cf5e760",
  "color": 7
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `title` | string | Yes | Column name |
| `boardId` | string | Yes | ID of the board to create column in |
| `color` | number | No | Color number (1-16) |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X POST "https://yougile.com/api-v2/columns" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "In Progress",
    "boardId": "0d923a9f-3675-43c6-84ce-f3580cf5e760",
    "color": 7
  }'
```

---

## Update Column

Update column details.

**Endpoint:** `PUT /api-v2/columns/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Column ID |

### Request Body

```json
{
  "title": "Done",
  "boardId": "new-board-id",
  "color": 5,
  "deleted": false
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `title` | string | No | Column name |
| `boardId` | string | No | Board ID (to move column) |
| `color` | number | No | Color number (1-16) |
| `deleted` | boolean | No | Set to true to delete |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X PUT "https://yougile.com/api-v2/columns/4f6f0391-0f94-4d30-9b0e-99430a36d4fb" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"title": "Completed", "color": 5}'
```
