# GovConnect roadmap

> Proposed plan. Dates are relative sprint days, not calendar commitments. Stories remain planned until implementation and acceptance criteria are verified.

## Epics

1. **Foundation / Infrastructure** — US-01 to US-03
2. **Authentication / Access Control** — US-04 to US-06
3. **Citizen Application Management** — US-07 to US-11
4. **Caseworker Review Workflow** — US-12 to US-15
5. **Administration & Audit** — US-16 to US-18
6. **Quality / Accessibility / Release** — US-19 to US-25

## Suggested 10-day sequence

| Day | Stories | Focus |
|---|---|---|
| 1 | US-01–US-02 | Repository baseline and PostgreSQL |
| 2 | US-03–US-05 | Schema, registration, authentication |
| 3 | US-06–US-07 | Authorization and app shell |
| 4 | US-08–US-09 | Application submission and listing |
| 5 | US-10–US-11 | Secure uploads and status history |
| 6 | US-12–US-14 | Review queue and decisions |
| 7 | US-15–US-18 | Additional information, administration, audit |
| 8 | US-19–US-20 | Accessibility and automated tests |
| 9 | US-21–US-23 | End-to-end/security checks, CI, startup validation |
| 10 | US-24–US-25 | Documentation and portfolio release |

## Suggested Kanban columns

- **Backlog** — captured, not yet ready
- **Ready** — acceptance criteria understood and dependencies clear
- **In Progress** — actively being implemented
- **In Review** — code/tests/docs awaiting review
- **Done** — acceptance criteria verified

## Working agreement

- Keep one issue per user story.
- Link pull requests to issues.
- Keep acceptance criteria as checkboxes and verify each before closing.
- Apply useful labels such as `feature`, `backend`, `frontend`, `database`, `security`, `testing`, `documentation`, `devops`, and `accessibility`.
- Record risks and deferred scope as issues instead of claiming unfinished features are complete.
