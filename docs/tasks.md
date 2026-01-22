# Tasks Endpoints

Tasks are the core work items in Yougile, placed within columns on boards.

## Get Tasks List

Get a list of tasks.

**Endpoint:** `GET /api-v2/task-list`

**Authentication:** Bearer token required

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `limit` | number | No | 50 | Number of items (max 1000) |
| `offset` | number | No | 0 | Index of first item |
| `title` | string | No | - | Filter by task title |
| `columnId` | string | No | - | Filter by column ID |
| `assignedTo` | string | No | - | Filter by assignee IDs (comma-separated) |
| `stickerId` | string | No | - | Filter by sticker ID |
| `stickerStateId` | string | No | - | Filter by sticker state ID |
| `includeDeleted` | boolean | No | false | Include deleted tasks |

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
      "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
      "title": "Implement feature",
      "description": "Task description text",
      "timestamp": 1623223299149,
      "columnId": "fefbc00f-3870-4f52-807f-225ce2e4c701",
      "deleted": false,
      "archived": false,
      "completed": false,
      "completedTimestamp": null,
      "assigned": ["80eed1bd-eda3-4991-ac17-09d28566749d"],
      "createdBy": "80eed1bd-eda3-4991-ac17-09d28566749d",
      "subtasks": ["sub-task-id-1", "sub-task-id-2"],
      "idTaskCommon": "ID-484",
      "idTaskProject": "DEV-484",
      "type": "task",
      "color": "task-primary",
      "deadline": {
        "deadline": 1653029146646,
        "startDate": 1653028146646,
        "withTime": true
      },
      "timeTracking": {
        "plan": 5,
        "work": 3
      },
      "stickers": {
        "sticker-id-1": "state-id-1",
        "sticker-id-2": "Custom value"
      },
      "checklists": [
        {
          "title": "Checklist 1",
          "items": [
            {"title": "Item 1", "isCompleted": false},
            {"title": "Item 2", "isCompleted": true}
          ]
        }
      ]
    }
  ]
}
```

### Task Colors

Available task card colors:
- `task-primary` - Default
- `task-gray`
- `task-red`
- `task-pink`
- `task-yellow`
- `task-green`
- `task-turquoise`
- `task-blue`
- `task-violet`

### Example

```bash
curl -X GET "https://yougile.com/api-v2/task-list" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

```bash
# Filter by column
curl -X GET "https://yougile.com/api-v2/task-list?columnId=COLUMN_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Get Task by ID

Get details of a specific task.

**Endpoint:** `GET /api-v2/tasks/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Task ID |

### Example

```bash
curl -X GET "https://yougile.com/api-v2/tasks/4f6f0391-0f94-4d30-9b0e-99430a36d4fb" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Create Task

Create a new task.

**Endpoint:** `POST /api-v2/tasks`

**Authentication:** Bearer token required

### Request Body

```json
{
  "title": "New Task",
  "columnId": "fefbc00f-3870-4f52-807f-225ce2e4c701",
  "description": "Task description",
  "assigned": ["user-id-1", "user-id-2"],
  "deadline": {
    "deadline": 1653029146646,
    "startDate": 1653028146646,
    "withTime": true,
    "blockedPoints": [],
    "links": []
  },
  "timeTracking": {
    "plan": 8,
    "work": 0
  },
  "checklists": [
    {
      "title": "Checklist",
      "items": [
        {"title": "Step 1", "isCompleted": false},
        {"title": "Step 2", "isCompleted": false}
      ]
    }
  ],
  "stickers": {
    "sticker-id": "state-id"
  },
  "color": "task-blue",
  "stopwatch": {
    "running": false
  },
  "timer": {
    "seconds": 3600,
    "running": false
  }
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `title` | string | Yes | Task title |
| `columnId` | string | No | Column ID to place task in |
| `description` | string | No | Task description |
| `assigned` | array | No | Array of user IDs to assign |
| `deadline` | object | No | Deadline sticker |
| `timeTracking` | object | No | Time tracking sticker |
| `checklists` | array | No | Checklist items |
| `stickers` | object | No | Custom sticker values |
| `color` | string | No | Task card color |
| `completed` | boolean | No | Mark as completed |
| `archived` | boolean | No | Archive the task |
| `subtasks` | array | No | Array of subtask IDs |
| `stopwatch` | object | No | Stopwatch sticker |
| `timer` | object | No | Timer sticker |

### Sticker Values

For custom stickers, the `stickers` object maps sticker IDs to values:
- State sticker: Use state ID as value (e.g., `"0baced9640b2"`)
- Empty sticker: Use `"empty"` to attach without state
- Text field: Use string value (e.g., `"Company Name"`)
- Number field: Use string number (e.g., `"123.45"`)

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X POST "https://yougile.com/api-v2/tasks" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "New Task",
    "columnId": "fefbc00f-3870-4f52-807f-225ce2e4c701"
  }'
```

---

## Update Task

Update task details.

**Endpoint:** `PUT /api-v2/tasks/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Task ID |

### Request Body

Same fields as create, plus:

```json
{
  "deleted": false,
  "columnId": "new-column-id",
  "deadline": {
    "deleted": true
  },
  "stickers": {
    "sticker-to-remove": "-"
  }
}
```

### Special Values

- To remove task from column: `"columnId": "-"`
- To remove a sticker: `"sticker-id": "-"`
- To remove deadline: `"deadline": {"deleted": true, "blockedPoints": [], "links": []}`
- To remove time tracking: `"timeTracking": {"deleted": true}`
- To remove timer: `"timer": {"deleted": true}`
- To remove stopwatch: `"stopwatch": {"deleted": true}`

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X PUT "https://yougile.com/api-v2/tasks/4f6f0391-0f94-4d30-9b0e-99430a36d4fb" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"completed": true}'
```

---

## Get Task Chat Subscribers

Get list of users subscribed to task chat.

**Endpoint:** `GET /api-v2/tasks/{id}/chat-subscribers`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Task ID |

### Response

```json
["user-id-1", "user-id-2"]
```

### Example

```bash
curl -X GET "https://yougile.com/api-v2/tasks/TASK_ID/chat-subscribers" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Update Task Chat Subscribers

Update the list of users subscribed to task chat.

**Endpoint:** `PUT /api-v2/tasks/{id}/chat-subscribers`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Task ID |

### Request Body

```json
{
  "content": ["user-id-1", "user-id-2", "user-id-3"]
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
curl -X PUT "https://yougile.com/api-v2/tasks/TASK_ID/chat-subscribers" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"content": ["user-id-1", "user-id-2"]}'
```
