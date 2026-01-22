# Sprint Stickers Endpoints

Sprint stickers are used for sprint/iteration tracking on tasks.

## Get Sprint Stickers List

Get a list of sprint stickers.

**Endpoint:** `GET /api-v2/sprint-stickers`

**Authentication:** Bearer token required

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `limit` | number | No | 50 | Number of items (max 1000) |
| `offset` | number | No | 0 | Index of first item |
| `name` | string | No | - | Filter by sticker name |
| `boardId` | string | No | - | Filter by board ID |
| `includeDeleted` | boolean | No | false | Include deleted stickers |

### Response

```json
{
  "paging": {
    "count": 2,
    "limit": 50,
    "offset": 0,
    "next": false
  },
  "content": [
    {
      "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
      "name": "Sprint",
      "deleted": false,
      "states": [
        {
          "id": "87ee83589735",
          "name": "Sprint 1",
          "deleted": false
        },
        {
          "id": "0baced9640b2",
          "name": "Sprint 2",
          "deleted": false
        }
      ]
    }
  ]
}
```

### Example

```bash
curl -X GET "https://yougile.com/api-v2/sprint-stickers" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

```bash
# Filter by board
curl -X GET "https://yougile.com/api-v2/sprint-stickers?boardId=BOARD_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Get Sprint Sticker by ID

Get details of a specific sprint sticker.

**Endpoint:** `GET /api-v2/sprint-stickers/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Sprint sticker ID |

### Example

```bash
curl -X GET "https://yougile.com/api-v2/sprint-stickers/STICKER_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Create Sprint Sticker

Create a new sprint sticker.

**Endpoint:** `POST /api-v2/sprint-stickers`

**Authentication:** Bearer token required

### Request Body

```json
{
  "name": "Sprint",
  "boardId": "board-id"
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | Yes | Sticker name |
| `boardId` | string | Yes | Board ID to attach sticker to |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X POST "https://yougile.com/api-v2/sprint-stickers" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"name": "Sprint", "boardId": "BOARD_ID"}'
```

---

## Update Sprint Sticker

Update a sprint sticker.

**Endpoint:** `PUT /api-v2/sprint-stickers/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Sprint sticker ID |

### Request Body

```json
{
  "name": "Updated Sprint Name"
}
```

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X PUT "https://yougile.com/api-v2/sprint-stickers/STICKER_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"name": "Iteration"}'
```

---

## Get Sprint State by ID

Get details of a specific sprint state.

**Endpoint:** `GET /api-v2/sprint-stickers/{stickerId}/states/{stickerStateId}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `stickerId` | string | Yes | Sprint sticker ID |
| `stickerStateId` | string | Yes | State ID |

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `includeDeleted` | boolean | No | false | Include if deleted |

### Response

```json
{
  "id": "87ee83589735",
  "name": "Sprint 1",
  "deleted": false
}
```

### Example

```bash
curl -X GET "https://yougile.com/api-v2/sprint-stickers/STICKER_ID/states/STATE_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Create Sprint State

Create a new sprint state.

**Endpoint:** `POST /api-v2/sprint-stickers/{stickerId}/states`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `stickerId` | string | Yes | Sprint sticker ID |

### Request Body

```json
{
  "name": "Sprint 3"
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | Yes | Sprint/state name |

### Response

```json
{
  "stickerStateId": "87ee83589735"
}
```

### Example

```bash
curl -X POST "https://yougile.com/api-v2/sprint-stickers/STICKER_ID/states" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"name": "Sprint 3"}'
```

---

## Update Sprint State

Update a sprint state.

**Endpoint:** `PUT /api-v2/sprint-stickers/{stickerId}/states/{stickerStateId}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `stickerId` | string | Yes | Sprint sticker ID |
| `stickerStateId` | string | Yes | State ID |

### Request Body

```json
{
  "name": "Sprint 3 - Extended"
}
```

### Response

```json
{
  "stickerStateId": "87ee83589735"
}
```

### Example

```bash
curl -X PUT "https://yougile.com/api-v2/sprint-stickers/STICKER_ID/states/STATE_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"name": "Sprint 3 - Extended"}'
```
