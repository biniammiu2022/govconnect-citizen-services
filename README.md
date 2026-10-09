# GovConnect — Citizen Services & Permits Management Platform

GovConnect is a portfolio project concept for a secure citizen-services portal where residents can submit service or permit applications, upload supporting documents, track progress, and receive decisions. Caseworkers review applications, while administrators manage access and inspect audit activity.

> **Project status:** Planning and initial backlog setup. Features listed below are the target scope, not a claim that they are already implemented. Update this README as working features are delivered and tested.

## Goals

- Provide a clear, accessible citizen application journey.
- Enforce authentication, role-based authorization, and per-user resource ownership.
- Support secure document uploads and controlled downloads.
- Give caseworkers a review queue and explicit decision workflow.
- Record status changes and security-relevant events for auditability.
- Maintain repeatable local setup, automated tests, and CI.

## Planned technology

- **Backend:** Java 21, Spring Boot, Spring Security
- **Frontend:** React, TypeScript, Vite
- **Database:** PostgreSQL with Flyway migrations
- **Testing:** JUnit, Spring testing, React Testing Library
- **Local development:** Docker Compose
- **CI:** GitHub Actions

## Target features

### Citizen
- Register and sign in
- Create service/permit applications
- Upload supporting documents
- Search applications and view current status/history
- Read requests for additional information and decisions

### Caseworker
- View a queue of applications requiring review
- Inspect application details and authorized attachments
- Request additional information
- Approve or reject eligible applications

### Administrator
- Search users and manage roles
- Review audit records and filter activity

### Engineering quality
- Server-side validation and authorization
- Safe file type/size handling and private document storage
- Accessible forms, keyboard navigation, and visible focus states
- Automated tests, CI, architecture documentation, and synthetic demo data

## Architecture (target)

```text
React + TypeScript (browser)
          |
          | HTTPS / JSON API
          v
Spring Boot REST API
  | Authentication / authorization
  | Application and review services
  | Audit events
  |
  +------ PostgreSQL (Flyway-managed schema)
  +------ Private document storage (not public web root)
```

The final authentication/session strategy, storage implementation, and API contract should be documented after implementation decisions are made.

## Repository layout (planned)

```text
backend/                 Spring Boot application and tests
frontend/                React + TypeScript application
database/migrations/     Database migration scripts
docs/                    Architecture, API examples, screenshots
.github/workflows/       CI workflow
docker-compose.yml       Local service orchestration
.env.example             Example configuration (no real secrets)
```

## Getting started

The application setup is still being built. Once the backend, frontend, and Compose configuration are committed, this section should contain verified commands for:

1. Installing Java 21, Node.js, and Docker.
2. Copying `.env.example` to a local `.env` and setting development-only values.
3. Starting PostgreSQL with Docker Compose.
4. Running Flyway migrations and starting the backend.
5. Installing frontend dependencies and starting Vite.
6. Running backend and frontend tests.

Do not put production credentials, tokens, or real citizen information in the repository.

## Backlog and planning

- [All GovConnect issues / user stories](https://github.com/biniammiu2022/govconnect-citizen-services/issues)
- [US-01 — Initialize repository and project structure](https://github.com/biniammiu2022/govconnect-citizen-services/issues/1)
- [US-02 — Run PostgreSQL with Docker Compose](https://github.com/biniammiu2022/govconnect-citizen-services/issues/2)
- [US-03 — Create initial database schema and migrations](https://github.com/biniammiu2022/govconnect-citizen-services/issues/3)

The 25 proposed user stories are grouped into six epics and sequenced across a suggested 10-day plan. Use issue acceptance criteria as the completion checklist, and only close stories when the criteria have been verified.

## Security notes

- Hash passwords using a suitable password encoder; never store plaintext passwords.
- Derive resource ownership from the authenticated principal, not a client-provided owner ID.
- Enforce authorization on every protected API and document download.
- Validate uploaded file size and content type; generate storage names and keep files private.
- Avoid logging passwords, tokens, or document contents.
- Use synthetic data in screenshots and demos.

## Testing and CI

Automated tests and a GitHub Actions workflow are planned. Add the exact commands and status badges only after the workflow is present and verified.

## Documentation

- `docs/architecture.md` — planned architecture and trust boundaries
- `docs/api-examples.md` — examples matching implemented endpoints
- `docs/roadmap.md` — epic breakdown and suggested 10-day schedule
- `docs/user-stories.md` — index of the 25 planned stories

## License

Choose and add a license before distributing or reusing the project.
