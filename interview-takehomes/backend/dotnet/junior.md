# Backend / .NET (ASP.NET Core) — Junior take-home

## Snapshot

| Field | Value |
| --- | --- |
| Track | Backend |
| Stack | ASP.NET Core (.NET 8), C# |
| Time box | 3–4 hours. Stop when the time is up. |
| Product | **Northline Notes** — personal notes API |
| Submit | Repo or zip + `NOTES.md` + how to run |

## Candidate brief

You are building **Northline Notes**, a tiny API for one user to keep notes.

A note has `title`, `body`, and `createdAt`. There is no real login. A header `x-user-id` is enough.

This is a take-home. Finish a thin slice you can run and click through with `curl` or an `.http` file.

### Time box

3–4 hours. If you run out of time, keep create + list working and write what you skipped.

### Rules of the exercise

- Use ASP.NET Core (minimal API or controllers — your choice).
- In-memory storage (or EF Core InMemory) is fine. SQLite or PostgreSQL is a plus if you already know it.
- Do not add IdentityServer, Redis, or Docker unless the core is done.
- Do not scaffold a full CRUD template and stop without reading it.

### Requirements

1. `POST /notes` — create a note. `title` is required (1–80 chars). `body` is optional (max 2000).
2. `GET /notes` — list notes for the current `x-user-id`, newest first.
3. `GET /notes/{id}` — one note. 404 if missing **or** if it belongs to another user id.
4. `PUT /notes/{id}` — update title and/or body. Same 404 rule.
5. `DELETE /notes/{id}` — delete. Same 404 rule.
6. Invalid body returns **400** with a readable message (a `ProblemDetails` / validation payload is a plus).
7. Seed 2–3 notes for user `u1` so list is not empty.

### Constraints

- Do not return another user’s note, even if they guess the id.
- Keep the happy path easy to run (`dotnet run`).
- `NOTES.md`: what you stored in memory vs a database, and one thing you would add next week.

### Deliverables

- Runnable API
- Seed or hardcoded start data
- `NOTES.md`

### Submission

Repo or zip. Include 5 `curl` (or `.http`) examples (create, list, get, update, delete).

---

## Stretch

Only if create/list/get already work:

- One automated test (xUnit) for 404 on another user’s id
- `GET /notes?q=` search on title
- A service class so the endpoint/controller is not doing everything
