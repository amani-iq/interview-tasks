# Backend / NestJS — Senior take-home

## Snapshot

| Field | Value |
| --- | --- |
| Track | Backend |
| Stack | NestJS, TypeScript, PostgreSQL |
| Time box | 6–8 hours. Stop when the time is up. |
| Product | **Northline Dispatch** — signed webhook intake and job routing |
| Submit | Repo or zip + `NOTES.md` + how to run |

## Candidate brief

You are building **Northline Dispatch**, an internal service that receives webhooks from payment and shipping vendors and turns them into work items for other teams.

Vendors retry. They send duplicates. Some payloads are hostile or huge. Your job is to accept work safely, not to build a full workflow engine.

This is a take-home. We would rather see a correct ingest path than five unfinished modules.

### Time box

6–8 hours. Prefer one production-shaped slice over a tour of NestJS features.

### Rules of the exercise

- Use NestJS + PostgreSQL.
- You may fake downstream workers (in-process, queue table, or BullMQ). Say why.
- Do not build a real vendor integration. Accept HTTP webhooks we can curl.
- Do not hide design choices in chat. Put them in `NOTES.md`.

### Requirements

Model at least two tenants (`acme`, `northline-shop`) and two vendors (`payments`, `shipping`).

Implement:

1. `POST /webhooks/:vendor`  
   - Verify an HMAC signature from a header (document the algorithm and what is signed).  
   - Reject unsigned, late, or oversized bodies with a stable error body.
2. **Idempotency** on a vendor-provided event id (header or payload). Retries must not create a second job.
3. Persist the raw event and a normalized `WorkItem` (`type`, `tenantId`, `status`, `attempts`).
4. A worker path that picks `pending` items and marks them `done` or `failed`. Simulate one downstream failure (e.g. shipping events with `simulateFailure: true`).
5. Retry policy: bounded retries + a terminal `dead` (or `poison`) state. Document the backoff, even if it is simple.
6. Admin read APIs (protect with a static admin token):  
   - list work items by tenant, vendor, status  
   - get one event + its work item history
7. Structured logs that include `tenantId`, `vendor`, `eventId`. No payload secrets in logs.
8. Tests: signature failure, duplicate event, retry-to-dead. These three matter more than snapshot tests.

### Constraints

- Tenants must not see each other’s events.
- Assume at-least-once delivery from vendors. Design for that, do not hope for exactly-once.
- If you use a queue, explain what happens when the process dies mid-handler.
- Keep the module graph boring and readable. Clever interceptors are not a substitute for a clear ingest use-case.

### Deliverables

- API + schema + seed
- Tests for the three cases above
- `NOTES.md`: threat model (short), failure modes, what you would add in week two
- Commands to run and to replay a duplicate webhook

### Submission

Repo or zip. Include a `curl` script that: sends a valid event, sends it again, sends a bad signature.

---

## Stretch

Only after the ingest path is trustworthy:

- Outbox or transactional enqueue so “saved event” and “queued work” cannot diverge
- Replay endpoint for a dead item
- OpenAPI and a rate limit per tenant
- A metric or log you would alert on (duplicate storm, dead-letter growth)
