# GovConnect architecture (target design)

> This document describes the intended architecture. Update it to match the implementation as it evolves.

## Components

- **React + TypeScript + Vite:** citizen and staff interfaces, accessible forms, application lists, review queue, and audit search.
- **Spring Boot REST API:** validation, business rules, authentication, authorization, workflow transitions, and audit events.
- **Spring Security:** authentication and role/ownership checks.
- **PostgreSQL:** user accounts, applications, document metadata, status history, reviews, and audit records.
- **Flyway:** version-controlled schema migrations.
- **Private file storage:** uploaded content outside the public web root or in access-controlled object storage.
- **Docker Compose:** repeatable local dependencies.
- **GitHub Actions:** backend tests, frontend tests/build, and quality checks.

## Request flow

1. Browser sends an HTTPS request to the REST API.
2. Security filters authenticate the caller.
3. Endpoint/service checks role and resource ownership.
4. Application service validates input and performs the permitted state transition.
5. PostgreSQL stores application data and relevant history/audit records.
6. API returns a response DTO without internal secrets or unnecessary sensitive fields.

## Roles and boundaries

- **Citizen:** can create and read their own applications, upload permitted documents, and view status/history.
- **Caseworker:** can access assigned/eligible review work and take permitted workflow actions.
- **Admin:** can manage user roles and search audit records.
- Every API request and document download must independently enforce authorization. Hiding a UI control is not an authorization boundary.

## Security considerations

- Use a vetted password encoder and never store plaintext passwords.
- Use the authenticated principal to determine ownership; do not trust owner IDs supplied by a browser.
- Validate inputs server-side and use DTOs rather than exposing persistence entities directly.
- Validate uploaded file size and content; generate safe storage names and store files privately.
- Record actor, action, target, timestamp, and safe metadata for relevant events.
- Never log passwords, access tokens, document contents, or unnecessary personal data.
- Configure secrets through environment variables or a secrets manager; commit only placeholders.
- Use synthetic data in demos and screenshots.

## Key data concepts

- **User:** identity, password hash, account status, role(s), timestamps.
- **ServiceRequest:** owner, service type, submitted fields, current status, timestamps.
- **Document:** request association, private storage key, safe original filename/metadata, content type, size.
- **StatusHistory / Review:** prior and current statuses, actor, reason/message, timestamp.
- **AuditEvent:** actor, action, target, timestamp, and redacted contextual metadata.

## Operational concerns

- Apply migrations automatically or as a documented deployment step.
- Add database health checks and structured logs without sensitive payloads.
- Test authentication, cross-user access denial, role boundaries, invalid transitions, and unsafe uploads.
- Document the chosen session/token strategy, CSRF/CORS settings, retention rules, and backup strategy once decided.
