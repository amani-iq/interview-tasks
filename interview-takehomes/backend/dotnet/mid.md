# Backend / .NET (ASP.NET Core) — Mid take-home

## Snapshot

| Field | Value |
| --- | --- |
| Track | Backend |
| Stack | ASP.NET Core (.NET 8), C#, PostgreSQL (or SQLite if they explain why) |
| Time box | 4–6 hours. Stop when the time is up. |
| Product | **Northline Leave Desk** — team leave requests |
| Submit | Repo or zip + `NOTES.md` + how to run |

## Candidate brief

You are building a small internal API for **Northline Leave Desk**.

Employees request time off. A manager approves or rejects. Two people on the same team should not be off on the same day if the team is marked `coverageRequired: true`. Each employee has a yearly leave balance.

This is a take-home, not a production launch. We care more about how you think than how many endpoints you add.

### Time box

4–6 hours. If you run out of time, ship a thinner vertical slice and write what you would do next in `NOTES.md`.

### Rules of the exercise

- Use ASP.NET Core.
- You may use EF Core or Dapper.
- Auth can be simple: a header like `x-user-id` plus a seeded admin user is fine. Say what you would replace it with.
- Do not spend time on a polished admin UI.
- Do not scaffold a generated CRUD project and stop.

### Requirements

Seed at least:

- 1 team with `coverageRequired: true`
- 2 employees on that team
- 1 manager who can approve
- yearly balances (e.g. 20 days)

Implement:

1. Create a leave request (`startDate`, `endDate`, `type`: `vacation` | `sick`).
2. Reject the request if it overlaps an **approved** request for the same employee.
3. Reject the request if it would put two **approved** absences on the same team-day when `coverageRequired` is true.
4. Reject the request if remaining yearly balance is not enough (count weekdays only).
5. Manager can `approve` or `reject` a pending request. Approval must re-check the same rules (the world may have changed).
6. List requests with filters: `employeeId`, `status`, date range.
7. At least one automated test around the coverage / overlap rule. That test is more important than 80% coverage.

### Constraints

- Dates are calendar dates, not timestamps. Be explicit about timezone (UTC dates are fine).
- Return structured errors (`code`, `message`, `details`). Do not leak stack traces.
- Keep the code split by domain, not by “controllers / services / everything”.
- README or `NOTES.md` must include: assumptions, tradeoffs, and what you skipped.

### Deliverables

- Runnable API (`docker compose` is a plus, not required)
- Migrations or seed script
- Tests for the core rule
- `NOTES.md` (1 page is enough)

### Submission

Send a GitHub/GitLab link or a zip. Include the exact commands to migrate, seed, and run.

---

## Stretch

Only if the core works and time remains. These are how we see above-mid thinking:

- Prevent double-approve of the same request
- Idempotent create (`Idempotency-Key`)
- Swagger/OpenAPI that matches the real errors
- A short note on how you would stop two overlapping approvals under concurrent requests
