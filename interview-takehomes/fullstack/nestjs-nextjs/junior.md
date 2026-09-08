# Fullstack / NestJS + Next.js — Junior take-home

## Snapshot

| Field | Value |
| --- | --- |
| Track | Fullstack |
| Stack | NestJS API + Next.js (App Router) UI |
| Time box | 4–5 hours. Stop when the time is up. |
| Product | **Northline Board** — one-team task list |
| Submit | Repo or zip + `NOTES.md` + how to run |

## Candidate brief

You are building **Northline Board**, a single shared task list for a tiny team.

A task has `title` and `done`. Anyone using the app shares the same list (no auth).

You must have a **real NestJS API** the Next.js UI calls. In-memory on the server is fine. Do not keep the only copy of data in React state.

### Time box

4–5 hours. One vertical slice (API + UI) beats a pretty frontend with fake arrays.

### Rules of the exercise

- Frontend: Next.js.
- Backend: a **NestJS** API. Next.js Route Handlers are not a substitute.
- In-memory on the NestJS side is fine. SQLite is optional.
- Do not add login, Docker Compose clusters, or a design system.

### Requirements

1. API (NestJS):
   - `GET /tasks` — list
   - `POST /tasks` — create (`title` required)
   - `PATCH /tasks/:id` — toggle or set `done`
   - `DELETE /tasks/:id` — delete, 404 if missing
2. UI:
   - List tasks from the API
   - Add task form
   - Toggle done
   - Delete
   - Loading state while the first list loads
   - Error text if the API is down
3. Refresh the browser: tasks are still there (until the server process restarts, if memory-only — say so).
4. Seed 2 tasks on server start.

### Constraints

- The UI must not be the source of truth.
- Title validation on the API (a DTO/pipe), not only in the input tag.
- `NOTES.md`: how to run the **NestJS API** and the **Next.js** app, CORS or proxy, and where data lives.

### Deliverables

- Runnable project(s)
- `NOTES.md` + example API requests

### Submission

Repo or zip. Include commands so a reviewer can see the list in the browser and via `curl`.

---

## Stretch

Only if the loop works:

- Disable the add button while the request is in flight
- 400 body that the form can show under the title field
- Split a Nest `TasksModule` (controller + service) so the controller stays thin
