# Users (Employees) Endpoints

## Get Users List

Get a list of employees in the company.

**Endpoint:** `GET /api-v2/users`

**Authentication:** Bearer token required

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `limit` | number | No | 50 | Number of items (max 1000) |
| `offset` | number | No | 0 | Index of first item |
| `email` | string | No | - | Filter by employee email |
| `projectId` | string | No | - | Filter by project ID |

### Response

```json
{
  "paging": {
    "count": 10,
    "limit": 50,
    "offset": 0,
    "next": false
  },
  "content": [
    {
      "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
      "email": "user@example.com",
      "isAdmin": false,
      "realName": "John Doe",
      "status": "online",
      "lastActivity": 1656012328
    }
  ]
}
```

### Example

```bash
curl -X GET "https://yougile.com/api-v2/users" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

```bash
# Filter by email
curl -X GET "https://yougile.com/api-v2/users?email=user@example.com" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Get User by ID

Get details of a specific user.

**Endpoint:** `GET /api-v2/users/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | User ID |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
  "email": "user@example.com",
  "isAdmin": false,
  "realName": "John Doe",
  "status": "online",
  "lastActivity": 1656012328
}
```

### Example

```bash
curl -X GET "https://yougile.com/api-v2/users/4f6f0391-0f94-4d30-9b0e-99430a36d4fb" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Invite User to Company

Invite a new user to the company.

**Endpoint:** `POST /api-v2/users`

**Authentication:** Bearer token required

### Request Body

```json
{
  "email": "newuser@example.com",
  "isAdmin": false
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `email` | string | Yes | Email address of the user to invite |
| `isAdmin` | boolean | No | Whether user should have admin rights |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X POST "https://yougile.com/api-v2/users" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"email": "newuser@example.com", "isAdmin": false}'
```

---

## Update User

Update user details.

**Endpoint:** `PUT /api-v2/users/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | User ID |

### Request Body

```json
{
  "isAdmin": true
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `isAdmin` | boolean | No | Whether user should have admin rights |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X PUT "https://yougile.com/api-v2/users/4f6f0391-0f94-4d30-9b0e-99430a36d4fb" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"isAdmin": true}'
```

---

## Delete User from Company

Remove a user from the company.

**Endpoint:** `DELETE /api-v2/users/{id}`

**Authentication:** Bearer token required

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | User ID |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X DELETE "https://yougile.com/api-v2/users/4f6f0391-0f94-4d30-9b0e-99430a36d4fb" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```
