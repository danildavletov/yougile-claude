# Authentication Endpoints

## Get Companies List

Get a list of companies accessible to the user.

**Endpoint:** `POST /api-v2/auth/companies`

**Authentication:** None (uses login/password in body)

### Query Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `limit` | number | No | 50 | Number of items (max 1000) |
| `offset` | number | No | 0 | Index of first item |

### Request Body

```json
{
  "login": "user@example.com",
  "password": "your_password",
  "name": "Company Name"  // optional - filter by name
}
```

### Response

```json
{
  "paging": {
    "count": 1,
    "limit": 50,
    "offset": 0,
    "next": false
  },
  "content": [
    {
      "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
      "name": "My Company",
      "isAdmin": true
    }
  ]
}
```

### Example

```bash
curl -X POST "https://yougile.com/api-v2/auth/companies" \
  -H "Content-Type: application/json" \
  -d '{"login": "user@example.com", "password": "secret"}'
```

---

## Get API Keys List

Get a list of existing API keys.

**Endpoint:** `POST /api-v2/auth/keys/get`

**Authentication:** None (uses login/password in body)

### Request Body

```json
{
  "login": "user@example.com",
  "password": "your_password",
  "companyId": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"  // optional
}
```

### Response

```json
[
  {
    "key": "H6HngIA816fpIhY7tBvWx/it3YbVvEt/33Sk8afA39MCR9a",
    "companyId": "858c5d32-dd93-4d2b-9b9c-aa1ec7007c0c",
    "timestamp": 1560506639447,
    "deleted": false
  }
]
```

### Example

```bash
curl -X POST "https://yougile.com/api-v2/auth/keys/get" \
  -H "Content-Type: application/json" \
  -d '{"login": "user@example.com", "password": "secret"}'
```

---

## Create API Key

Create a new API key for a specific company.

**Endpoint:** `POST /api-v2/auth/keys`

**Authentication:** None (uses login/password in body)

### Request Body

```json
{
  "login": "user@example.com",
  "password": "your_password",
  "companyId": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Response

```json
{
  "key": "H6HngIA816fpIhY7tBvWx/it3YbVvEt/33Sk8afA39MCR9a"
}
```

### Example

```bash
curl -X POST "https://yougile.com/api-v2/auth/keys" \
  -H "Content-Type: application/json" \
  -d '{
    "login": "user@example.com",
    "password": "secret",
    "companyId": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
  }'
```

---

## Delete API Key

Delete an existing API key.

**Endpoint:** `DELETE /api-v2/auth/keys/{key}`

**Authentication:** None

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `key` | string | Yes | The API key to delete |

### Response

Status 200 on success.

### Example

```bash
curl -X DELETE "https://yougile.com/api-v2/auth/keys/H6HngIA816fpIhY7tBvWx%2Fit3YbVvEt%2F33Sk8afA39MCR9a"
```

Note: URL-encode the key if it contains special characters like `/` or `+`.
