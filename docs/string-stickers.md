# String Stickers Endpoints

String stickers (also called "stickers with states") are custom labels that can be attached to tasks with predefined states/values.

## Get String Stickers List

Get a list of string stickers.

**Endpoint:** `GET /api-v2/string-stickers`

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
    "count": 3,
    "limit": 50,
    "offset": 0,
    "next": false
  },
  "content": [
    {
      "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
      "name": "Priority",
      "icon": "star",
      "deleted": false,
      "states": [
        {
          "id": "87ee83589735",
          "name": "High",
          "color": "#EB3737",
          "deleted": false
        },
        {
          "id": "0baced9640b2",
          "name": "Medium",
          "color": "#FCE258",
          "deleted": false
        },
        {
          "id": "815016901edd",
          "name": "Low",
          "color": "#7CAE5E",
          "deleted": false
        }
      ]
    }
  ]
}
```

### Available Icons

`star`, `heart`, `check`, `cloud`, `filter`, `alarm`, `bolt`, `bookmark`, `box`, `bulb`, `prio`, `code`, `ruble`, `dollar`, `euro`, `eye`, `flag`, `flame`, `history`, `info`, `key`, `anchor`, `message`, `movie`, `mnote`, `pencil`, `percent`, `phone`, `pin`, `price`, `return`, `rocket`, `smile`, `tag`, `user`, `group`, `warning`

### Example

```bash
curl -X GET "https://yougile.com/api-v2/string-stickers" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

```bash
# Filter by board
curl -X GET "https://yougile.com/api-v2/string-stickers?boardId=BOARD_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Get String Sticker by ID

Get details of a specific string sticker.

**Endpoint:** `GET /api-v2/string-stickers/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Sticker ID |

### Example

```bash
curl -X GET "https://yougile.com/api-v2/string-stickers/STICKER_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Create String Sticker

Create a new string sticker.

**Endpoint:** `POST /api-v2/string-stickers`

**Authentication:** Bearer token required

### Request Body

```json
{
  "name": "Priority",
  "icon": "star",
  "boardId": "board-id"
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | Yes | Sticker name |
| `icon` | string | No | Icon name (see available icons above) |
| `boardId` | string | Yes | Board ID to attach sticker to |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X POST "https://yougile.com/api-v2/string-stickers" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Priority",
    "icon": "star",
    "boardId": "BOARD_ID"
  }'
```

---

## Update String Sticker

Update a string sticker.

**Endpoint:** `PUT /api-v2/string-stickers/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Sticker ID |

### Request Body

```json
{
  "name": "Updated Name",
  "icon": "flag"
}
```

### Example

```bash
curl -X PUT "https://yougile.com/api-v2/string-stickers/STICKER_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"name": "New Priority"}'
```

---

## Get Sticker State by ID

Get details of a specific sticker state.

**Endpoint:** `GET /api-v2/string-stickers/{stickerId}/states/{stickerStateId}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `stickerId` | string | Yes | Sticker ID |
| `stickerStateId` | string | Yes | State ID |

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `includeDeleted` | boolean | No | false | Include if deleted |

### Response

```json
{
  "id": "87ee83589735",
  "name": "High",
  "color": "#EB3737",
  "deleted": false
}
```

### Example

```bash
curl -X GET "https://yougile.com/api-v2/string-stickers/STICKER_ID/states/STATE_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Create Sticker State

Create a new state for a string sticker.

**Endpoint:** `POST /api-v2/string-stickers/{stickerId}/states`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `stickerId` | string | Yes | Sticker ID |

### Request Body

```json
{
  "name": "Critical",
  "color": "#EB3737"
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | Yes | State name |
| `color` | string | No | Hex color code (e.g., "#EB3737") |

### Response

```json
{
  "stickerStateId": "87ee83589735"
}
```

### Example

```bash
curl -X POST "https://yougile.com/api-v2/string-stickers/STICKER_ID/states" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"name": "Critical", "color": "#EB3737"}'
```

---

## Update Sticker State

Update a sticker state.

**Endpoint:** `PUT /api-v2/string-stickers/{stickerId}/states/{stickerStateId}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `stickerId` | string | Yes | Sticker ID |
| `stickerStateId` | string | Yes | State ID |

### Request Body

```json
{
  "name": "Updated Name",
  "color": "#5089F2"
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
curl -X PUT "https://yougile.com/api-v2/string-stickers/STICKER_ID/states/STATE_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"name": "Very High", "color": "#EB3737"}'
```
