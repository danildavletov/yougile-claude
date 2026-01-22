# Yougile API Overview

## Base URL

```
https://yougile.com/api-v2
```

## Authentication

All API requests (except authentication endpoints) require an API key passed as a Bearer token in the Authorization header:

```
Authorization: Bearer <your_api_key>
Content-Type: application/json
```

### Getting an API Key

1. **Get Company ID**: Use `POST /api-v2/auth/companies` with your login/password to get a list of companies and their IDs
2. **Create API Key**: Use `POST /api-v2/auth/keys` with login, password, and companyId to generate an API key
3. **Use the Key**: Include the key in all subsequent requests

Alternative: Get Company ID using keyboard shortcut in Yougile interface (Ctrl+Alt+Q / Ctrl+Option+Q for Mac)

## Rate Limits

- Maximum 50 requests per minute per company
- Each account can have up to 30 API keys

## Common Response Codes

| Code | Description |
|------|-------------|
| 200 | Success |
| 201 | Created (for POST requests) |
| 400 | Bad request |
| 401 | Unauthorized (invalid credentials) |
| 403 | Forbidden (insufficient permissions) |
| 404 | Not found |
| 429 | Rate limit exceeded |

## Pagination

List endpoints support pagination with these query parameters:

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `limit` | number | 50 | Number of items per page (max 1000) |
| `offset` | number | 0 | Index of first item |

Response includes paging metadata:
```json
{
  "paging": {
    "count": 25,
    "limit": 50,
    "offset": 0,
    "next": false
  },
  "content": [...]
}
```

## Soft Delete

Most entities support soft delete. By default, deleted objects are not returned. Use `includeDeleted=true` query parameter to include deleted objects in results.

## Permissions

The API respects account permissions. If a user cannot perform an action through the UI due to insufficient permissions, the same restriction applies via API.

## Common Request Example

```bash
curl -X GET "https://yougile.com/api-v2/projects" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

## Common Create/Update Example

```bash
curl -X POST "https://yougile.com/api-v2/projects" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"title": "New Project"}'
```
