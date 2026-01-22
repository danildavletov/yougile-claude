# Departments Endpoints

Departments allow organizing employees into hierarchical groups.

## Get Departments List

Get a list of departments in the company.

**Endpoint:** `GET /api-v2/departments`

**Authentication:** Bearer token required

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `limit` | number | No | 50 | Number of items (max 1000) |
| `offset` | number | No | 0 | Index of first item |
| `title` | string | No | - | Filter by department name |
| `parentId` | string | No | - | Filter by parent department ID |
| `includeDeleted` | boolean | No | false | Include deleted departments |

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
      "title": "Development",
      "parentId": "001623dc-6501-461b-9de6-c1d1d6fc1d16",
      "deleted": false,
      "users": {
        "4902b994-b806-4af4-acec-018ea5ea6468": "manager",
        "8aeaeb9d-f94e-4c66-96d3-eb8d96fe7018": "member"
      }
    }
  ]
}
```

### User Roles in Departments

- `manager` - Department manager
- `member` - Department member

### Example

```bash
curl -X GET "https://yougile.com/api-v2/departments" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Get Department by ID

Get details of a specific department.

**Endpoint:** `GET /api-v2/departments/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Department ID |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
  "title": "Development",
  "parentId": "001623dc-6501-461b-9de6-c1d1d6fc1d16",
  "deleted": false,
  "users": {
    "4902b994-b806-4af4-acec-018ea5ea6468": "manager"
  }
}
```

### Example

```bash
curl -X GET "https://yougile.com/api-v2/departments/4f6f0391-0f94-4d30-9b0e-99430a36d4fb" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Create Department

Create a new department.

**Endpoint:** `POST /api-v2/departments`

**Authentication:** Bearer token required

### Request Body

```json
{
  "title": "Development",
  "parentId": "001623dc-6501-461b-9de6-c1d1d6fc1d16",
  "users": {
    "4902b994-b806-4af4-acec-018ea5ea6468": "manager",
    "8aeaeb9d-f94e-4c66-96d3-eb8d96fe7018": "member"
  }
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `title` | string | Yes | Department name |
| `parentId` | string | No | Parent department ID. Leave empty or set to "-" for top-level |
| `users` | object | No | Map of user IDs to roles (manager/member) |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X POST "https://yougile.com/api-v2/departments" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"title": "Development"}'
```

---

## Update Department

Update department details.

**Endpoint:** `PUT /api-v2/departments/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Department ID |

### Request Body

```json
{
  "title": "Updated Name",
  "parentId": "new-parent-id",
  "users": {
    "4902b994-b806-4af4-acec-018ea5ea6468": "manager",
    "user-to-remove": "-"
  },
  "deleted": false
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `title` | string | No | Department name |
| `parentId` | string | No | Parent department ID |
| `users` | object | No | Map of user IDs to roles |
| `deleted` | boolean | No | Set to true to delete |

### Removing Users

To remove a user from the department, set their role to `"-"` or empty string `""`:

```json
{
  "users": {
    "user-id-to-remove": "-"
  }
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
curl -X PUT "https://yougile.com/api-v2/departments/4f6f0391-0f94-4d30-9b0e-99430a36d4fb" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"title": "Engineering"}'
```
