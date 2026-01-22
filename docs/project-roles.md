# Project Roles Endpoints

Custom project roles allow fine-grained permission control for users within a project.

## Get Project Roles List

Get a list of custom roles in a project.

**Endpoint:** `GET /api-v2/projects/{projectId}/roles`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project ID |

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `limit` | number | No | 50 | Number of items (max 1000) |
| `offset` | number | No | 0 | Index of first item |
| `name` | string | No | - | Filter by role name |

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
      "name": "Consultant",
      "description": "General consulting role",
      "permissions": {
        "editTitle": true,
        "delete": false,
        "addBoard": true,
        "boards": {
          "editTitle": true,
          "delete": false,
          "move": false,
          "showStickers": true,
          "editStickers": false,
          "addColumn": true,
          "settings": false,
          "columns": {
            "editTitle": true,
            "delete": false,
            "move": "no",
            "addTask": true,
            "allTasks": { ... },
            "withMeTasks": { ... },
            "myTasks": { ... },
            "createdByMeTasks": { ... }
          }
        },
        "children": {}
      }
    }
  ]
}
```

### Example

```bash
curl -X GET "https://yougile.com/api-v2/projects/PROJECT_ID/roles" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Get Project Role by ID

Get details of a specific project role.

**Endpoint:** `GET /api-v2/projects/{projectId}/roles/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project ID |
| `id` | string | Yes | Role ID |

### Example

```bash
curl -X GET "https://yougile.com/api-v2/projects/PROJECT_ID/roles/ROLE_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Create Project Role

Create a new custom role in a project.

**Endpoint:** `POST /api-v2/projects/{projectId}/roles`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project ID |

### Request Body

```json
{
  "name": "Consultant",
  "description": "General consulting role",
  "permissions": {
    "editTitle": true,
    "delete": false,
    "addBoard": true,
    "boards": {
      "editTitle": true,
      "delete": false,
      "move": false,
      "showStickers": true,
      "editStickers": false,
      "addColumn": true,
      "settings": false,
      "columns": {
        "editTitle": true,
        "delete": false,
        "move": "no",
        "addTask": true,
        "allTasks": {
          "show": true,
          "delete": false,
          "editTitle": true,
          "editDescription": true,
          "complete": true,
          "close": false,
          "assignUsers": "no",
          "connect": false,
          "editSubtasks": "no",
          "editStickers": false,
          "editPins": false,
          "move": "no",
          "sendMessages": true,
          "sendFiles": true,
          "editWhoToNotify": "no"
        },
        "withMeTasks": { ... },
        "myTasks": { ... },
        "createdByMeTasks": { ... }
      }
    },
    "children": {}
  }
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | Yes | Role name |
| `description` | string | No | Role description |
| `permissions` | object | Yes | Permission settings |

### Task Permission Values

For `assignUsers`:
- `no` - Cannot assign
- `yes` - Can assign anyone
- `add-self` - Can add self
- `set-self` - Can set self as assignee
- `change-from-self` - Can change from self

For `editSubtasks`:
- `no` - Cannot edit
- `yes` - Full edit
- `complete` - Can only complete

For `move`:
- `no` - Cannot move
- `project` - Within project
- `yes` - Anywhere
- `board` - Within board (tasks only)

For `editWhoToNotify`:
- `no` - Cannot edit
- `yes` - Can edit all
- `self` - Can add/remove self

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X POST "https://yougile.com/api-v2/projects/PROJECT_ID/roles" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"name": "Consultant", "permissions": {...}}'
```

---

## Update Project Role

Update an existing project role.

**Endpoint:** `PUT /api-v2/projects/{projectId}/roles/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project ID |
| `id` | string | Yes | Role ID |

### Request Body

Same structure as create, all fields optional.

### Example

```bash
curl -X PUT "https://yougile.com/api-v2/projects/PROJECT_ID/roles/ROLE_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"name": "Updated Role Name"}'
```

---

## Delete Project Role

Delete a project role.

**Endpoint:** `DELETE /api-v2/projects/{projectId}/roles/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project ID |
| `id` | string | Yes | Role ID |

### Response

Returns the deleted role object.

### Example

```bash
curl -X DELETE "https://yougile.com/api-v2/projects/PROJECT_ID/roles/ROLE_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```
