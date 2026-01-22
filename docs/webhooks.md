# Webhooks Endpoints

Webhooks allow you to receive notifications when events occur in your Yougile company.

## Get Webhooks List

Get a list of webhook subscriptions.

**Endpoint:** `GET /api-v2/webhooks`

**Authentication:** Bearer token required

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `includeDeleted` | boolean | No | false | Include deleted webhooks |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
  "url": "https://your-server.com/webhook",
  "events": ["task.created", "task.updated"],
  "deleted": false
}
```

### Example

```bash
curl -X GET "https://yougile.com/api-v2/webhooks" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Create Webhook

Create a new webhook subscription.

**Endpoint:** `POST /api-v2/webhooks`

**Authentication:** Bearer token required

### Request Body

```json
{
  "url": "https://your-server.com/webhook",
  "events": ["task.created", "task.updated", "task.deleted"]
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `url` | string | Yes | URL to receive webhook notifications |
| `events` | array | Yes | List of events to subscribe to |

### Available Events

Common event types include:
- `task.created` - Task created
- `task.updated` - Task updated
- `task.deleted` - Task deleted
- `project.created` - Project created
- `project.updated` - Project updated
- `board.created` - Board created
- `board.updated` - Board updated
- `column.created` - Column created
- `column.updated` - Column updated
- `message.created` - Message sent

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X POST "https://yougile.com/api-v2/webhooks" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://your-server.com/webhook",
    "events": ["task.created", "task.updated"]
  }'
```

---

## Update Webhook

Update a webhook subscription.

**Endpoint:** `PUT /api-v2/webhooks/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Webhook ID |

### Request Body

```json
{
  "url": "https://new-server.com/webhook",
  "events": ["task.created"]
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `url` | string | No | Updated webhook URL |
| `events` | array | No | Updated list of events |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X PUT "https://yougile.com/api-v2/webhooks/WEBHOOK_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"events": ["task.created", "task.updated", "task.deleted"]}'
```

---

## Webhook Payload

When an event occurs, Yougile sends a POST request to your webhook URL with a JSON payload:

```json
{
  "event": "task.created",
  "timestamp": 1653029146646,
  "data": {
    "id": "task-id",
    "title": "Task title",
    ...
  }
}
```

### Handling Webhooks

Your webhook endpoint should:
1. Return a 2xx status code quickly (within a few seconds)
2. Process the payload asynchronously if needed
3. Handle duplicate deliveries (implement idempotency)

### Retry Policy

If your endpoint doesn't respond with a 2xx status code, Yougile may retry the webhook delivery.
