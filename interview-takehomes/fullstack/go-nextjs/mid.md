# Fullstack / Go + Next.js — Mid take-home

## Snapshot

| Field | Value |
| --- | --- |
| Track | Fullstack |
| Stack | Go API + Next.js (App Router) |
| Time box | 5–7 hours. Stop when the time is up. |
| Product | **Northline Desk + Leave** — UI on top of leave requests |
| Submit | Repo or zip + `NOTES.md` + how to run |

## Candidate brief

You are building a small internal tool for **Northline Leave Desk**.

Employees create leave requests. A manager approves or rejects. Two people on the same team must not both be **approved** off on the same day if the team is `coverageRequired: true`. Each employee has a yearly balance (weekdays only).

The **API owns the rules**. The UI must show API errors in human language.

### Time box

5–7 hours. Prefer a working employee + manager path over a pixel-perfect design.

### Rules of the exercise

- Next.js for the UI.
- **Go** for the API (`net/http` or a small router). Rules live in Go, not in Route Handlers.
- Auth can be a user picker or `x-user-id` / cookie. Seed an employee and a manager.
- Do not spend the session on SSO.

### Requirements

1. Seed: 1 coverage-required team, 2 employees, 1 manager, balances (e.g. 20 days).
2. API:
   - Create request (`startDate`, `endDate`, `type`: `vacation` | `sick`)
   - Reject overlap on the same employee (vs **approved** requests)
   - Reject team coverage conflict
   - Reject if weekday balance is not enough
   - Manager approve/reject; **approve re-checks rules**
   - List with filters: status, employee
   - Structured errors (`code`, `message`)
3. UI:
   - Employee: create + see my requests
   - Manager: list pending + approve/reject
   - Date validation in the form (end ≥ start) **and** server errors shown if the API refuses
   - Empty and error states
4. At least one API test for the coverage/overlap rule.

### Constraints

- Do not only disable the submit button and call that “the rule”.
- Dates as calendar dates; say timezone (UTC is fine).
- `NOTES.md`: how to run API + web, assumptions, what you would do for real auth.

### Deliverables

- Two processes or a monorepo with scripts
- Seed
- Test for the core rule
- `NOTES.md`

### Submission

Repo or zip. Include two logins/ids (employee, manager) and a scenario that should fail coverage.

---

## Stretch

Only if the main path works:

- Filters in the URL on the manager list
- Re-fetch after approve so the employee view is not stale
- Shared error-code list the UI maps to copy
- `go test` for the coverage rule plus a short note on CORS/proxy
