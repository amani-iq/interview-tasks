# Backend / NestJS — Junior take-home

## Snapshot

| Field | Value |
| --- | --- |
| Track | Backend |
| Stack | NestJS, TypeScript |
| Time box | 3–4 hours. Stop when the time is up. |
| Product | **Northline Notes** — personal notes API |
| Submit | Repo or zip + `NOTES.md` + how to run |

## Candidate brief

You are building **Northline Notes**, a tiny API for one user to keep notes.

A note has `title`, `body`, and `createdAt`. There is no real login. A header `x-user-id` is enough.

This is a take-home. Finish a thin slice you can run and click through with `curl` or HTTP files.

### Time box

3–4 hours. If you run out of time, keep create + list working and write what you skipped.

### Rules of the exercise

- Use NestJS.
- In-memory storage is fine. SQLite or PostgreSQL is a plus if you already know it.
- Do not add JWT, Redis, Docker, or Swagger unless the core is done.
- Do not paste a generated resource and stop without reading it.

### Requirements

1. `POST /notes` — create a note. `title` is required (1–80 chars). `body` is optional (max 2000).
2. `GET /notes` — list notes for the current `x-user-id`, newest first.
3. `GET /notes/:id` — one note. 404 if missing **or** if it belongs to another user id.
4. `PATCH /notes/:id` — update title and/or body. Same 404 rule.
5. `DELETE /notes/:id` — delete. Same 404 rule.
6. Invalid body returns **400** with a readable message (field errors are a plus).
7. Seed 2–3 notes for user `u1` so list is not empty.

### Constraints

- Do not return another user’s note, even if they guess the id.
- Keep the happy path easy to run (`npm install`, `npm run start:dev`).
- `NOTES.md`: what you stored in memory vs a database, and one thing you would add next week.

### Deliverables

- Runnable API
- Seed or hardcoded start data
- `NOTES.md`

### Submission

Repo or zip. Include 5 `curl` examples (create, list, get, patch, delete).

---

## Stretch

Only if create/list/get already work:

- One automated test for 404 on another user’s id
- `GET /notes?q=` search on title
- A `Note` module with controller + service (not all logic in the controller)
