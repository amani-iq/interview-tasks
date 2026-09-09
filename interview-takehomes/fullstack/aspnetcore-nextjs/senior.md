# Fullstack / ASP.NET Core + Next.js — Senior take-home

## Snapshot

| Field | Value |
| --- | --- |
| Track | Fullstack |
| Stack | ASP.NET Core (.NET 8, PostgreSQL) API + Next.js (App Router) UI |
| Time box | 7–9 hours. Stop when the time is up. |
| Product | **Northline Atlas Dispatch** — tenant ops UI on signed ingest |
| Submit | Repo or zip + `NOTES.md` + how to run |

## Candidate brief

You are building **Northline Atlas** on top of **Northline Dispatch**.

Vendors send signed webhooks to an ASP.NET Core API. The API stores events and work items. Ops users in a **workspace** inspect events, retry dead items, and must never see another workspace’s data.

Vendors retry. Users open two tabs. Your job is a trustworthy slice, not a full incident platform.

### Time box

7–9 hours. One production-shaped path (ingest → persist → tenant UI → retry) beats five unfinished modules.

### Rules of the exercise

- **ASP.NET Core** + PostgreSQL for ingest and reads.
- Next.js App Router for the ops UI.
- Auth can be a mocked session and two users in two workspaces. Seed them.
- Fake vendors: `curl` + HMAC. No real Stripe/shipping.

### Requirements

1. **Ingest API** (`POST /webhooks/{vendor}`)
   - HMAC signature (document algorithm and signed string; constant-time compare)
   - Reject unsigned, late, or oversized bodies
   - Idempotency on vendor event id (retries = one work item)
   - Persist raw event + `WorkItem` (`pending` → `done` | `failed` → `dead`)
   - Bounded retries; one simulated failure path
2. **Tenant isolation**
   - Workspaces `acme` and `northline-shop`
   - Every list/detail query scoped by membership
   - Guessing another slug is 403/404, not an empty leak
3. **Ops UI** (`/w/[workspaceSlug]/...`)
   - Workspace in the URL (source of truth)
   - Event/work-item list with status filter (URL params)
   - Detail: payload metadata (no secrets), status history
   - Retry action for `dead` items
   - After retry or a new webhook, the list must update in a way you can explain (revalidate/tag or documented client cache)
4. **Logs:** `tenantId`, `vendor`, `eventId`. No raw secrets.
5. **Tests (API):** bad signature, duplicate event, user A denied workspace B (or equivalent query test).
6. `NOTES.md`: threat model (short), cache/invalidation, crash mid-handler, week-two list.

### Constraints

- At-least-once from vendors. Do not claim exactly-once if you did not build it.
- UI must not bundle other tenants’ records.
- Prefer a monorepo or two folders with one `README` and clear scripts (background worker included).
- Include a `curl` script: valid event, duplicate, bad signature.

### Deliverables

- API + schema + seed
- UI with two users / two workspaces
- Tests above
- `NOTES.md` + runbook (how to start both, how to replay)

### Submission

Repo or zip. Include accounts, two workspace URLs, and the curl script.

---

## Stretch

Only after ingest + tenancy are real:

- Outbox so “saved event” and “queued work” cannot diverge
- Replay vs retry distinction
- Rate limit per tenant
- Loading UI that does not flash the wrong workspace name
