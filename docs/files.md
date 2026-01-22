# File Upload Endpoint

## Upload File

Upload a file to the server and get its URL.

**Endpoint:** `POST /api-v2/upload-file`

**Authentication:** Bearer token required

**Content-Type:** `multipart/form-data`

### Request

Send the file as form data with the key `file`.

**Important:** When using curl from command line, do not explicitly specify the `boundary` in Content-Type - curl will set the appropriate header automatically.

### Response

```json
{
  "result": "ok",
  "url": "/user-data/8d046ef2-e069-4ae0-b575-0d932639358e/file.png",
  "fullUrl": "https://example.com/user-data/8d046ef2-e069-4ae0-b575-0d932639358e/file.png"
}
```

| Field | Type | Description |
|-------|------|-------------|
| `result` | string | Upload result status |
| `url` | string | Relative URL of the uploaded file |
| `fullUrl` | string | Full URL of the uploaded file |

### Example

```bash
curl -X POST "https://yougile.com/api-v2/upload-file" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -F "file=@/path/to/your/file.png"
```

### Usage in Tasks

After uploading a file, you can use the returned URL in task descriptions or chat messages. The file URL can be embedded in markdown format:

```markdown
![Image description](https://example.com/user-data/.../file.png)
```

Or as a link:

```markdown
[Download file](https://example.com/user-data/.../file.pdf)
```
