# Company Endpoints

## Get Company Details

Get details of the current company (associated with the API key).

**Endpoint:** `GET /api-v2/companies*`

**Authentication:** Bearer token required

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
  "title": "My Company",
  "timestamp": 1623223299149,
  "deleted": false,
  "apiData": {}
}
```

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Company ID |
| `title` | string | Company name |
| `timestamp` | number | Creation timestamp |
| `deleted` | boolean | Whether the company is deleted |
| `apiData` | object | Auxiliary data for development |

### Example

```bash
curl -X GET "https://yougile.com/api-v2/companies*" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Update Company

Update company details.

**Endpoint:** `PUT /api-v2/companies*`

**Authentication:** Bearer token required

### Request Body

```json
{
  "title": "New Company Name",
  "apiData": {}
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `title` | string | No | Company name |
| `deleted` | boolean | No | Set to true to delete |
| `apiData` | object | No | Auxiliary data for development |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb"
}
```

### Example

```bash
curl -X PUT "https://yougile.com/api-v2/companies*" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"title": "New Company Name"}'
```
