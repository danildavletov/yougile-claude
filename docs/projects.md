# Projects Endpoints

## Get Projects List

Get a list of projects in the company.

**Endpoint:** `GET /api-v2/projects`

**Authentication:** Bearer token required

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `limit` | number | No | 50 | Number of items (max 1000) |
| `offset` | number | No | 0 | Index of first item |
| `title` | string | No | - | Filter by project name |
| `includeDeleted` | boolean | No | false | Include deleted projects |

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
      "title": "My Project",
      "timestamp": 1623223299149,
      "deleted": false,
      "users": {
        "4902b994-b806-4af4-acec-018ea5ea6468": "worker",
        "8aeaeb9d-f94e-4c66-96d3-eb8d96fe7018": "admin"
      }
    }
  ]
}
```

### User Roles

The `users` object maps user IDs to their roles:
- `admin` - Project administrator
- `worker` - Regular worker
- `observer` - Observer (read-only)
- Custom role ID (UUID) - Custom project role

### Example

```bash
curl -X GET "https://yougile.com/api-v2/projects" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

```bash
# Filter by title
curl -X GET "https://yougile.com/api-v2/projects?title=Marketing" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Get Project by ID

Get details of a specific project.

**Endpoint:** `GET /api-v2/projects/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Project ID |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
  "title": "My Project",
  "timestamp": 1623223299149,
  "deleted": false,
  "users": {
    "4902b994-b806-4af4-acec-018ea5ea6468": "worker"
  }
}
```

### Example

```bash
curl -X GET "https://yougile.com/api-v2/projects/4f6f0391-0f94-4d30-9b0e-99430a36d4fb" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Create Project

Create a new project.

**Endpoint:** `POST /api-v2/projects`

**Authentication:** Bearer token required

### Request Body

```json
{
  "title": "New Project",
  "users": {
    "4902b994-b806-4af4-acec-018ea5ea6468": "worker",
    "8aeaeb9d-f94e-4c66-96d3-eb8d96fe7018": "admin"
  }
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `title` | string | Yes | Project name |
| `users` | object | No | Map of user IDs to roles |

### User Role Values

- `admin` - Project administrator
- `worker` - Regular worker
- `observer` - Observer (read-only)
- Custom role ID - ID of a custom project role

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X POST "https://yougile.com/api-v2/projects" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "New Project",
    "users": {"80eed1bd-eda3-4991-ac17-09d28566749d": "admin"}
  }'
```

---

## Update Project

Update project details.

**Endpoint:** `PUT /api-v2/projects/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Project ID |

### Request Body

```json
{
  "title": "Updated Project Name",
  "users": {
    "4902b994-b806-4af4-acec-018ea5ea6468": "admin",
    "8aeaeb9d-f94e-4c66-96d3-eb8d96fe7018": "-"
  },
  "deleted": false
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `title` | string | No | Project name |
| `users` | object | No | Map of user IDs to roles |
| `deleted` | boolean | No | Set to true to delete |

### Removing Users

To remove a user from the project, set their role to `"-"`:

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
curl -X PUT "https://yougile.com/api-v2/projects/4f6f0391-0f94-4d30-9b0e-99430a36d4fb" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"title": "Updated Project Name"}'
```
