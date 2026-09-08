# Backend / Go — Junior take-home

## Snapshot

| Field | Value |
| --- | --- |
| Track | Backend |
| Stack | Go 1.22+ |
| Time box | 3–4 hours. Stop when the time is up. |
| Product | **Northline Locker** — item check-in API |
| Submit | Repo or zip + `NOTES.md` + how to run |

## Candidate brief

You are building **Northline Locker**, a tiny API for a front desk.

People check an item in (`name`, `owner`) and later check it out. An item is either `held` or `released`.

This is a take-home. A boring `net/http` service is enough.

### Time box

3–4 hours. If time is short, finish check-in + list + checkout.

### Rules of the exercise

- Standard library is enough. A small router is fine.
- In-memory map is fine. Say that it is not durable.
- Do not add gRPC, Docker, or an ORM.
- `go test ./...` should run.

### Requirements

1. `POST /items` — check in. `name` and `owner` required. Status starts `held`. Return the created item with an `id`.
2. `GET /items` — list all, optional `?status=held` or `released`.
3. `GET /items/{id}` — one item or 404.
4. `POST /items/{id}/release` — mark `released`. Second release is **409**. Unknown id is **404**.
5. Invalid JSON or missing fields → **400** (not a panic, not 500).
6. At least one test: release twice → 409 (or the service error you map to 409).

### Constraints

- No `log.Fatal` inside handlers.
- Keep `main` small. Handlers or a small server type should be readable.
- `NOTES.md`: how to run, and what you would persist.

### Deliverables

- Runnable server (`go run .`)
- Test above
- `NOTES.md`

### Submission

Repo or zip. Include `curl` for check-in, list, release, release-again.

---

## Stretch

Only if the core works:

- Mutex around the map (we will ask why)
- Filter by `owner`
- Table-driven tests for 400/404/409
