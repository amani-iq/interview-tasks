# Frontend / Next.js — Senior take-home

## Snapshot

| Field | Value |
| --- | --- |
| Track | Frontend |
| Stack | Next.js (App Router), TypeScript, React |
| Time box | 6–8 hours. Stop when the time is up. |
| Product | **Northline Atlas** — multi-workspace ops dashboard |
| Submit | Repo or zip + `NOTES.md` + how to run |

## Candidate brief

You are building **Northline Atlas**, an internal ops dashboard used by more than one workspace.

Each workspace has services, incidents, and members. Switching workspace must change **every** surface: nav badge, list data, incident detail, and settings. No leftover data from the last workspace.

Auth can be a mocked session (cookie or header) with two users in two workspaces. Hard-code users in seed data.

### Time box

6–8 hours. One coherent multi-workspace slice beats five pages of disconnected widgets.

### Rules of the exercise

- Next.js App Router.
- Data can be local (SQLite, Drizzle, or a typed JSON store on the server).
- A design system or UI kit is allowed if you still own layout and state.
- Do not spend the exercise on a marketing landing page.

### Requirements

1. **Workspace switcher** in the shell. Active workspace is part of the URL (`/w/[workspaceSlug]/...`). Deep links must work.
2. **Services** (`/w/[slug]/services`) — list with status (`ok` | `degraded` | `down`). Filter in the URL.
3. **Incidents**  
   - List for the workspace.  
   - Create incident (title, severity, affected service ids).  
   - Detail with status timeline (`open` → `acknowledged` → `resolved`).  
   - Creating or updating an incident must update the services view without a full manual refresh story you cannot explain.
4. **Settings** (`/w/[slug]/settings`) — rename workspace display name. After save, the switcher and page titles must show the new name.
5. **Auth gate** — user A cannot open user B’s workspace by guessing the slug (404 or 403, not an empty leak).
6. Cross-route consistency: open services in one tab, resolve an incident in another (or via a second request). Document how you expect cache to behave. Implement at least one explicit revalidate/tag strategy.
7. Error and not-found that stay inside the workspace shell.
8. One automated test of tenancy (user A denied workspace B) **or** a Playwright test of switcher + rename.

### Constraints

- Workspace slug in the URL is the source of truth, not only React context.
- If you use client cache (SWR/React Query), explain it vs RSC cache. Pick one story and make it true.
- No secrets in client bundles. Seed passwords can be dummy; still do not expose other users’ records.
- Performance: do not download every workspace’s incidents to filter on the client.

### Deliverables

- Runnable app + seed (2 workspaces, 2 users, mixed services/incidents)
- `NOTES.md`: cache/invalidation, tenancy model, what you would add for real SSO
- Test as above

### Submission

Repo or zip. Include accounts to log in as and two URLs that must 403/404 for the other user.

---

## Stretch

Only after tenancy and cache are real:

- Optimistic timeline with conflict if two people resolve/ack
- `loading.tsx` that does not flash the wrong workspace name
- Partial prerender or a comment on why you would not
- A note on CSP / headers you would set in production
