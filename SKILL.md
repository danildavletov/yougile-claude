---
name: yougile
description: Interact with Yougile project management API. Use for managing projects, boards, tasks, stickers, chats, and more in Yougile.
argument-hint: "[request] api_key=KEY"
---

# Yougile API Skill

This skill enables interaction with the Yougile project management API. You can list, create, update, and manage projects, boards, tasks, stickers, chats, and more.

## User Request

$ARGUMENTS

## Parsing Arguments

Extract from the user's request above:
- **api_key**: Look for `api_key=VALUE` or `key=VALUE` pattern
- **Request**: Everything else describes what operation to perform
- **IDs**: Look for patterns like `board_id=`, `project_id=`, `task_id=`, or UUIDs

If no arguments provided or api_key is missing, ask the user interactively.

## Authentication

Before making API requests, the user must provide their Yougile API key:

```
api_key: YOUR_API_KEY_HERE
```

If the user doesn't have an API key, they can create one using the auth endpoints (requires Yougile login credentials).

## Base URL

All API requests use: `https://yougile.com/api-v2`

## Available Operations

### Read Operations (GET - No Confirmation Required)

| Category | Operations |
|----------|------------|
| **Company** | Get company details |
| **Users** | List users, get user by ID |
| **Projects** | List projects, get project by ID |
| **Project Roles** | List roles, get role by ID |
| **Departments** | List departments, get department by ID |
| **Boards** | List boards, get board by ID |
| **Columns** | List columns, get column by ID |
| **Tasks** | List tasks, get task by ID, get chat subscribers |
| **String Stickers** | List stickers, get sticker by ID, get state by ID |
| **Sprint Stickers** | List stickers, get sticker by ID, get state by ID |
| **Group Chats** | List chats, get chat by ID |
| **Chat Messages** | Get message history, get message by ID |
| **Webhooks** | List webhooks |
| **CRM** | Find contact by external ID |

### Write Operations (POST/PUT/DELETE - Confirmation Required)

| Category | Operations |
|----------|------------|
| **Auth** | Get companies (POST), get/create/delete API keys |
| **Company** | Update company |
| **Users** | Invite user, update user, delete user |
| **Projects** | Create project, update project |
| **Project Roles** | Create role, update role, delete role |
| **Departments** | Create department, update department |
| **Boards** | Create board, update board |
| **Columns** | Create column, update column |
| **Tasks** | Create task, update task, update chat subscribers |
| **String Stickers** | Create sticker, update sticker, create/update state |
| **Sprint Stickers** | Create sticker, update sticker, create/update state |
| **Group Chats** | Create chat, update chat |
| **Chat Messages** | Send message, update message |
| **Webhooks** | Create webhook, update webhook |
| **CRM** | Create contact person, create/update deals |
| **Files** | Upload file |

## Confirmation Requirement

**IMPORTANT:** All write operations (POST, PUT, DELETE) require explicit user confirmation before execution.

Before executing any write operation, present to the user:
1. The operation being performed
2. The endpoint and method
3. The request body (if applicable)
4. Ask: "Do you want to proceed with this operation?"

Only execute after receiving explicit confirmation.

## Executing Requests

Use curl via the Bash tool with these headers:

```bash
curl -X METHOD "https://yougile.com/api-v2/ENDPOINT" \
  -H "Authorization: Bearer API_KEY" \
  -H "Content-Type: application/json" \
  -d 'JSON_BODY'
```

## Documentation References

For detailed endpoint information, read the appropriate documentation file:

| Topic | Documentation File |
|-------|-------------------|
| API Overview & Auth basics | `docs/_overview.md` |
| Authentication endpoints | `docs/auth.md` |
| Users/Employees | `docs/users.md` |
| Company | `docs/company.md` |
| File upload | `docs/files.md` |
| Projects | `docs/projects.md` |
| Project Roles | `docs/project-roles.md` |
| Departments | `docs/departments.md` |
| Boards | `docs/boards.md` |
| Columns | `docs/columns.md` |
| Tasks | `docs/tasks.md` |
| String Stickers (with states) | `docs/string-stickers.md` |
| Sprint Stickers | `docs/sprint-stickers.md` |
| Group Chats | `docs/group-chats.md` |
| Chat Messages | `docs/chat-messages.md` |
| Webhooks | `docs/webhooks.md` |
| CRM | `docs/crm.md` |

When the user requests a specific operation, read the relevant documentation file to get the exact endpoint details, parameters, and request/response schemas.

## Example Workflows

### List Tasks in a Column

1. User provides: API key and column ID
2. Read `docs/tasks.md` for endpoint details
3. Execute: `GET /api-v2/task-list?columnId=COLUMN_ID`
4. Return formatted results

### Create a New Task

1. User provides: API key, column ID, task title
2. Read `docs/tasks.md` for create endpoint details
3. Show confirmation: "I will create task 'Title' in column X. Proceed?"
4. On confirmation, execute: `POST /api-v2/tasks` with JSON body
5. Return the new task ID

### Check and Create Stickers

1. User provides: API key, board ID, sticker name
2. Execute: `GET /api-v2/string-stickers?boardId=BOARD_ID&name=NAME`
3. If not found, show confirmation to create
4. On confirmation, execute: `POST /api-v2/string-stickers`

## Rate Limits

- Maximum 50 requests per minute per company
- Handle 429 responses by waiting before retrying

## Error Handling

Common error codes:
- 400: Bad request (check parameters)
- 401: Unauthorized (check API key)
- 403: Forbidden (insufficient permissions)
- 404: Resource not found
- 429: Rate limit exceeded (wait and retry)
