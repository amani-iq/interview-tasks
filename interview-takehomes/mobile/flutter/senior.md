# Mobile / Flutter — Senior take-home

## Snapshot

| Field | Value |
| --- | --- |
| Track | Mobile |
| Stack | Flutter, Dart |
| Time box | 6–8 hours. Stop when the time is up. |
| Product | **Northline Field** — offline-first site inspection |
| Submit | Repo or zip + `NOTES.md` + how to run |

## Candidate brief

You are building **Northline Field**, an inspection app for sites with bad cell coverage.

Inspectors create visits, fill a short form, and attach **one** photo (or a picked image / camera stub). Everything must work with airplane mode on. When connectivity returns, visits sync to a **fake** server you control in-process or via a local HTTP mock.

### Time box

6–8 hours. A truthful offline/sync story beats a pixel-perfect UI with `http` calls that fail silently.

### Rules of the exercise

- Flutter, latest stable.
- Fake server: in-memory + delay, or a local `shelf`/mock. Do not require our cloud.
- Architecture: you choose. We will ask you to defend it.
- Do not add real Firebase Auth or production maps.

### Requirements

1. **Visit list** with sync status per row: `local-only`, `syncing`, `synced`, `conflict`, `failed`.
2. **Create / edit visit** while offline: site name, result (`pass` | `fail` | `needs_work`), notes, one image. Save immediately to local storage.
3. **Sync engine** (not “save button = POST”):  
   - queue outbound changes  
   - retry failed network with backoff (can be simple)  
   - do not block the UI thread on image work if you can avoid it (isolate or a documented compromise)
4. **Conflict:** the fake server already has a visit with the same id and a newer `updatedAt` (seed this). Sync must not silently overwrite. Show a conflict screen: keep local, keep remote, or a merge you can explain.
5. Connectivity: a banner when offline. Creating a visit still works. Sync starts when you flip a “network on” toggle if you cannot read real connectivity in the environment — that toggle is acceptable if documented.
6. After process kill, queue and drafts are still there.
7. List stays usable with 50+ visits (build lazily). Do not decode giant images on the list (thumb or placeholder).
8. At least one test: conflict resolution **or** “offline create then sync produces one server record”.

### Constraints

- Local DB is the source of truth the UI reads. Network is a side effect.
- Never show `synced` if the server never got the payload.
- Errors must say whether the user should retry or wait.
- `NOTES.md` must include a sequence diagram for: offline create → online → conflict.

### Deliverables

- Flutter app + fake server + seed conflict
- Persistence that survives restart
- Test as above
- `NOTES.md`: sync model, thread/isolate choices, known holes

### Submission

Repo or zip. Include a script or README path: “turn network off, create visit, kill app, turn network on, see sync / conflict”.

---

## Stretch

Only after sync is truthful:

- Photo compression on an isolate
- Partial sync (notes yes, photo later) with status that reflects that
- Accessibility: status not color-only
- A second device story (even if simulated): two locals, one remote
