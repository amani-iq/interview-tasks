# Frontend / Next.js — Mid take-home

## Snapshot

| Field | Value |
| --- | --- |
| Track | Frontend |
| Stack | Next.js (App Router), TypeScript, React |
| Time box | 4–6 hours. Stop when the time is up. |
| Product | **Northline Desk** — internal ticket board |
| Submit | Repo or zip + `NOTES.md` + how to run |

## Candidate brief

You are building **Northline Desk**, a small internal tool for a support lead.

Tickets have `title`, `priority` (`low` | `normal` | `high`), `status` (`open` | `pending` | `closed`), `assignee`, and `updatedAt`. The lead filters the board, opens a ticket, and changes status.

Use local data (JSON file, SQLite, or in-memory on the server). No need for a real auth vendor.

### Time box

4–6 hours. A complete board + detail + status change beats a half-themed marketing shell.

### Rules of the exercise

- Next.js App Router.
- You may style with CSS modules, Tailwind, or vanilla CSS. Make it look like an internal tool, not a template gallery.
- Do not add NextAuth, Prisma, and tRPC unless they help you finish the product.
- Do not use a UI kit dump as the whole submission.

### Requirements

1. **Board page** (`/`)  
   - List tickets.  
   - Filter by status and priority. Filters must live in the **URL** (`searchParams`) so refresh keeps them.  
   - Sort by `updatedAt` descending.  
   - Empty state when filters match nothing.
2. **Detail page** (`/tickets/[id]`)  
   - Full ticket.  
   - Change status. After save, the board should show the new status (no stale client cache story without a comment).
3. **Create ticket** — a page or modal. Validate title (required, max 80 chars).
4. Loading and error UI for list and detail (App Router conventions or an equivalent you can explain).
5. Keyboard: filters and the status control must be usable without a mouse.
6. Seed 8–12 tickets so the board is not empty.

### Constraints

- Say what runs on the server vs the client, in `NOTES.md` or code comments.
- Do not fetch your own Route Handlers from a Server Component without a reason.
- Visual design should feel like a desk tool: dense, readable, calm. No hero section.

### Deliverables

- Runnable `npm`/`pnpm` app
- Seed data
- `NOTES.md`: tradeoffs, what you would do with a real API, known a11y gaps

### Submission

Repo or zip. Include Node version and `pnpm dev` / `npm run dev`.

---

## Stretch

Only if the core feels done:

- Optimistic status change with rollback on failure
- `useTransition` or similar pending state that does not block the whole page
- Basic filter announce for screen readers
- A test (Playwright or Testing Library) on filter + status change
