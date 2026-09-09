# Backend / PHP (Laravel) — Junior take-home

## Snapshot

| Field | Value |
| --- | --- |
| Track | Backend |
| Stack | PHP 8.2+, Laravel 11 |
| Time box | 3–4 hours. Stop when the time is up. |
| Product | **Northline Notes** — personal notes API |
| Submit | Repo or zip + `NOTES.md` + how to run |

## Candidate brief

You are building **Northline Notes**, a tiny API for one user to keep notes.

A note has `title`, `body`, and `created_at`. There is no real login. A header `x-user-id` is enough.

This is a take-home. Finish a thin slice you can run and click through with `curl`.

### Time box

3–4 hours. If you run out of time, keep create + list working and write what you skipped.

### Rules of the exercise

- Use Laravel.
- SQLite is fine (and simplest). MySQL/PostgreSQL is a plus if you already know it.
- Do not add Sanctum/Passport, Redis, or Docker unless the core is done.
- Do not scaffold a full CRUD generator and stop without reading it.

### Requirements

1. `POST /api/notes` — create a note. `title` is required (1–80 chars). `body` is optional (max 2000).
2. `GET /api/notes` — list notes for the current `x-user-id`, newest first.
3. `GET /api/notes/{id}` — one note. 404 if missing **or** if it belongs to another user id.
4. `PUT /api/notes/{id}` — update title and/or body. Same 404 rule.
5. `DELETE /api/notes/{id}` — delete. Same 404 rule.
6. Invalid body returns **422** with a readable message (Laravel validation errors are fine).
7. Seed 2–3 notes for user `u1` so list is not empty.

### Constraints

- Do not return another user’s note, even if they guess the id.
- Keep the happy path easy to run (`php artisan migrate --seed`, `php artisan serve`).
- `NOTES.md`: which database you used and one thing you would add next week.

### Deliverables

- Runnable API
- Migration + seeder
- `NOTES.md`

### Submission

Repo or zip. Include 5 `curl` examples (create, list, get, update, delete).

---

## Stretch

Only if create/list/get already work:

- One automated test (Pest/PHPUnit) for 404 on another user’s id
- `GET /api/notes?q=` search on title
- A Form Request for validation and a small service class (keep the controller thin)
