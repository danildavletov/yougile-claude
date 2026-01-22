# CRM Endpoints

CRM (Customer Relationship Management) endpoints for managing contacts, organizations, and deals.

## Create Contact Person

Create a new contact person in CRM.

**Endpoint:** `POST /api-v2/crm/contact-persons`

**Authentication:** Bearer token required

### Request Body

```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "phone": "+1234567890"
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | Yes | Contact name |
| `email` | string | No | Contact email |
| `phone` | string | No | Contact phone |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
  "name": "John Doe",
  "email": "john@example.com",
  "phone": "+1234567890"
}
```

### Example

```bash
curl -X POST "https://yougile.com/api-v2/crm/contact-persons" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com"
  }'
```

---

## Find Contact by External ID

Find a CRM contact by external messenger ID.

**Endpoint:** `GET /api-v2/crm/contacts/by-external-id`

**Authentication:** Bearer token required

### Query Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `provider` | string | Yes | External integration provider (e.g., "wazzup") |
| `chatId` | string | Yes | Chat ID in external messenger |

### Response

```json
{
  "id": "4f6f0391-0f94-4d30-9b0e-99430a36d4fb",
  "name": "Contact Name",
  "type": "contact"
}
```

### Example

```bash
curl -X GET "https://yougile.com/api-v2/crm/contacts/by-external-id?provider=wazzup&chatId=chat-123" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## CRM Deals (via Tasks)

CRM deals are created as special tasks. To create a deal, use the task creation endpoint with CRM-specific fields.

### Creating a Deal

**Endpoint:** `POST /api-v2/tasks`

```json
{
  "title": "New Deal - Company ABC",
  "columnId": "crm-board-column-id",
  "deal": {
    "dealAmount": 25000,
    "contactPersonIds": ["contact-id-1", "contact-id-2"],
    "organizationId": "org-id",
    "customFields": {
      "fieldId1": "value1",
      "fieldId2": "value2"
    }
  }
}
```

### Deal Fields

| Field | Type | Description |
|-------|------|-------------|
| `dealAmount` | number | Deal amount/value |
| `contactPersonIds` | array | Array of contact person IDs |
| `organizationId` | string | Organization ID |
| `customFields` | object | Custom CRM fields (fieldId -> value) |

### Updating Deal Data

**Endpoint:** `PUT /api-v2/tasks/{id}`

```json
{
  "deal": {
    "dealAmount": 30000,
    "contactPersonIds": ["contact-id-1"],
    "organizationId": null,
    "customFields": {
      "fieldId1": "updated-value"
    }
  }
}
```

### Special Values for Updates

- Set `dealAmount` to `null` to remove the amount
- Set `contactPersonIds` to `[]` to remove all contacts
- Set `organizationId` to `null` to unlink organization

### Example: Create Deal

```bash
curl -X POST "https://yougile.com/api-v2/tasks" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Sales Deal - ABC Corp",
    "columnId": "CRM_COLUMN_ID",
    "deal": {
      "dealAmount": 50000,
      "contactPersonIds": ["CONTACT_ID"]
    }
  }'
```

### Example: Update Deal Amount

```bash
curl -X PUT "https://yougile.com/api-v2/tasks/TASK_ID" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "deal": {
      "dealAmount": 75000
    }
  }'
```
