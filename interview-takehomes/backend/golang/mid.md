# Backend / Go — Mid take-home

## Snapshot

| Field | Value |
| --- | --- |
| Track | Backend |
| Stack | Go 1.22+ |
| Time box | 4–6 hours. Stop when the time is up. |
| Product | **Northline Courier** — package checkpoints |
| Submit | Repo or zip + `NOTES.md` + how to run |

## Candidate brief

You are building **Northline Courier**, a tiny backend that records package checkpoints.

A package is created with a destination. Scanners post checkpoints (`picked_up`, `in_transit`, `arrived`, `delivered`). The package must not move backwards, and `delivered` is terminal.

This is a take-home. A boring, correct service beats a microservice diagram.

### Time box

4–6 hours. If time is short, keep storage in memory **and say what you would persist**.

### Rules of the exercise

- Standard library is enough. A router like `chi` or `echo` is fine.
- No ORM required.
- Do not add gRPC, Kafka, or a full observability stack unless it helps you finish the core.
- `go test ./...` should pass.

### Requirements

1. `POST /packages` — create a package (`id` optional, `destination` required). Start status `created`.
2. `POST /packages/{id}/checkpoints` — append a checkpoint with `status` and `scannedAt`.
3. Enforce the allowed transitions:

   `created → picked_up → in_transit → arrived → delivered`

   `in_transit` may repeat (multiple hubs). Nothing else may go backwards. `delivered` accepts no further checkpoints.
4. `GET /packages/{id}` — current status + checkpoint history, oldest first.
5. `GET /packages?status=` — filter. Pagination can be a simple `limit`/`offset`.
6. A small **async** path: when a package becomes `delivered`, enqueue a “notify destination desk” job. A background worker prints or stores the notification. The HTTP handler must not do the notification inline.
7. Table-driven tests for: happy path, illegal transition, checkpoint after delivered.

### Constraints

- Use `context.Context` on service methods.
- Return errors the handler can map to 400/404/409. Do not `log.Fatal` in request paths.
- Protect in-memory maps with a mutex if you use them. We will race it mentally.
- Keep packages small: `http`, `service`, `store` (names can differ). Avoid a 400-line `main`.

### Deliverables

- `README` or `NOTES.md`: how to run, assumptions, what you would persist
- Tests as above
- A way to start HTTP + worker together

### Submission

Repo or zip. Include `go test ./...` and the command that starts the server.

---

## Stretch

Only if the core is done:

- Graceful shutdown: finish in-flight requests, drain the notify queue, then exit
- File or SQLite persistence
- `Idempotency-Key` on checkpoint create (scanners retry)
- A race test (`-race`) that still passes
