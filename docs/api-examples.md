# API examples (planned contract)

> These are design examples, not a claim that these endpoints already exist. Treat the implementation and integration tests as the source of truth; revise paths and payloads when the API is implemented.

## Authentication and identity

| Method | Example path | Purpose | Access |
|---|---|---|---|
| POST | `/api/auth/register` | Create a citizen account | Public |
| POST | `/api/auth/login` | Authenticate | Public |
| POST | `/api/auth/logout` | End session, if cookie/session auth is chosen | Authenticated |
| GET | `/api/users/me` | Current account profile | Authenticated |

## Citizen applications

| Method | Example path | Purpose | Access |
|---|---|---|---|
| POST | `/api/requests` | Submit a request | Citizen |
| GET | `/api/requests` | List own requests with filters | Citizen |
| GET | `/api/requests/{id}` | Read own request details | Owner or authorized staff |
| GET | `/api/requests/{id}/history` | Read status history | Owner or authorized staff |
| POST | `/api/requests/{id}/documents` | Upload supporting document | Owner or authorized staff |
| GET | `/api/documents/{id}/download` | Download a document after authorization | Authorized user |

## Caseworker and admin workflows

| Method | Example path | Purpose | Access |
|---|---|---|---|
| GET | `/api/staff/requests` | Review queue | Caseworker/Admin |
| POST | `/api/staff/requests/{id}/approve` | Approve eligible request | Caseworker/Admin |
| POST | `/api/staff/requests/{id}/reject` | Reject eligible request | Caseworker/Admin |
| POST | `/api/staff/requests/{id}/request-information` | Ask citizen for more information | Caseworker/Admin |
| GET | `/api/admin/users` | Search accounts | Admin |
| PATCH | `/api/admin/users/{id}/role` | Change permitted role | Admin |
| GET | `/api/admin/audit-events` | Search audit history | Admin |

## Example request payloads

Register (illustrative only):

```json
{
  "email": "demo.citizen@example.test",
  "password": "replace-with-a-local-test-password",
  "displayName": "Demo Citizen"
}
```

Create an application (illustrative only; owner is derived from the authenticated identity):

```json
{
  "serviceType": "BUILDING_PERMIT",
  "title": "Residential deck permit",
  "description": "Request for a small residential deck."
}
```

Request additional information (illustrative only):

```json
{
  "message": "Please attach the updated site plan."
}
```

## API conventions to implement

- Validate request bodies server-side and return consistent field-level validation errors.
- Use HTTP status codes consistently (for example, 201 for creation, 400 for invalid input, 401 for unauthenticated, 403 for unauthorized, and 404 when appropriate).
- Never accept citizen ownership from an untrusted request body.
- Check authorization on every document download and staff action.
- Prevent invalid or repeated workflow state transitions.
- Keep API responses free of password hashes, tokens, internal storage paths, and unnecessary personal data.
