# Fullstack / PHP (Laravel) + Next.js — Junior take-home

## Snapshot

| Field | Value |
| --- | --- |
| Track | Fullstack |
| Stack | Laravel API + Next.js (App Router) UI |
| Time box | 4–5 hours. Stop when the time is up. |
| Product | **Northline Board** — one-team task list |
| Submit | Repo or zip + `NOTES.md` + how to run |

## Candidate brief

You are building **Northline Board**, a single shared task list for a tiny team.

A task has `title` and `done`. Anyone using the app shares the same list (no auth).

You must have a **real Laravel API** the Next.js UI calls. SQLite on the server is fine. Do not keep the only copy of data in React state.

### Time box

4–5 hours. One vertical slice (API + UI) beats a pretty frontend with fake arrays.

### Rules of the exercise

- Frontend: Next.js.
- Backend: a **Laravel** API. Next.js Route Handlers are not a substitute.
- SQLite on the Laravel side is fine.
- Do not add login, Docker Compose clusters, or a design system.

### Requirements

1. API (Laravel):
   - `GET /api/tasks` — list
   - `POST /api/tasks` — create (`title` required)
   - `PATCH /api/tasks/{id}` — toggle or set `done`
   - `DELETE /api/tasks/{id}` — delete, 404 if missing
2. UI:
   - List tasks from the API
   - Add task form
   - Toggle done
   - Delete
   - Loading state while the first list loads
   - Error text if the API is down
3. Refresh the browser: tasks are still there (persisted in the DB).
4. Seed 2 tasks.

### Constraints

- The UI must not be the source of truth.
- Title validation on the API (a Form Request / validation), not only in the input tag.
- `NOTES.md`: how to run the **Laravel API** and the **Next.js** app, CORS or proxy, and where data lives.

### Deliverables

- Runnable project(s)
- `NOTES.md` + example API requests

### Submission

Repo or zip. Include commands so a reviewer can see the list in the browser and via `curl`.

---

## Stretch

Only if the loop works:

- Disable the add button while the request is in flight
- 422 body that the form can show under the title field
- A small service or action so the controller stays thin
