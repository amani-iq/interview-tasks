# Backend / Go — Senior take-home

## Snapshot

| Field | Value |
| --- | --- |
| Track | Backend |
| Stack | Go 1.22+ |
| Time box | 6–8 hours. Stop when the time is up. |
| Product | **Northline Relay** — concurrent event ingest |
| Submit | Repo or zip + `NOTES.md` + how to run |

## Candidate brief

You are building **Northline Relay**, an ingest service used by store devices.

Devices POST small JSON events (`deviceId`, `type`, `occurredAt`, `payload`). The HTTP process must stay responsive. Heavy work (validate, enrich, “write” to a sink) happens in a worker pool.

We will judge the concurrency model more than the business domain.

### Time box

6–8 hours. A complete ingest + pool + sink beats an unfinished platform.

### Rules of the exercise

- Standard library preferred. Small extras are fine if you justify them.
- The sink can be a file, SQLite, or an in-memory store that fakes I/O latency.
- Do not add Kubernetes manifests or a service mesh.
- `go test ./...` and `go test -race ./...` should be part of your story.

### Requirements

1. `POST /events` — accept an event, return quickly with an ack id. Do **not** do enrichment on the request goroutine.
2. Bounded worker pool (configurable `N` workers, bounded queue).
3. **Backpressure:** when the queue is full, fail the HTTP request with `503` + `Retry-After` (or a documented equivalent). Do not grow memory without a cap.
4. Enrichment (can be fake): attach `receivedAt`, lowercase `type`, reject unknown types with a **non-retryable** error.
5. Sink writes: simulate slow I/O (e.g. 20–50ms). Retry sink errors a bounded number of times. Then mark the event failed and continue. One bad event must not stall the pool.
6. `GET /healthz` — process up. `GET /readyz` — accepting work (not shutting down, queue not permanently wedged).
7. Graceful shutdown on SIGINT/SIGTERM: stop accepting, drain or fail queued work **on purpose**, wait for in-flight workers with a timeout, then exit.
8. Stats endpoint or log line: accepted, queued, processed, failed, rejected-full.
9. Tests:  
   - full queue returns 503  
   - unknown type does not retry forever  
   - shutdown does not leak goroutines (a test or a clear argument + `goleak` is excellent)

### Constraints

- Every worker must honor `context` cancel.
- Document what is lost on crash. Do not claim durability you did not build.
- No unbounded `go func()` per event.
- HTTP timeouts should exist, even if simple.

### Deliverables

- Runnable server + config via flags or env
- Tests above
- `NOTES.md`: concurrency diagram (ASCII is fine), lost-work cases, what you would persist next

### Submission

Repo or zip. Include a small script or `README` section that floods `/events` until 503 appears.

---

## Stretch

Only after the pool behaves:

- Persistent queue (disk) and what that changes about 503
- Per-`deviceId` ordering while keeping global parallelism
- pprof notes: what you would look at if queue latency climbs
- Explicit poison-queue file for failed events
