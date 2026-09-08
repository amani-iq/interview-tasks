# Frontend / Next.js — Junior take-home

## Snapshot

| Field | Value |
| --- | --- |
| Track | Frontend |
| Stack | Next.js (App Router), TypeScript, React |
| Time box | 3–4 hours. Stop when the time is up. |
| Product | **Northline Shelf** — personal reading list |
| Submit | Repo or zip + `NOTES.md` + how to run |

## Candidate brief

You are building **Northline Shelf**, a small reading list.

A book has `title`, `author`, and `status` (`want` | `reading` | `done`). Data can live in React state, `localStorage`, or a JSON file. No login.

This is a take-home. Make it usable, not a marketing site.

### Time box

3–4 hours. A working add + list beats a custom design system.

### Rules of the exercise

- Next.js App Router.
- CSS modules, Tailwind, or plain CSS. Keep it simple.
- Do not add auth, Prisma, or a component library dump as the whole app.

### Requirements

1. **List page** (`/`) — all books. Show title, author, status.
2. **Add book** — form on `/` or `/new`. Title and author required. Status defaults to `want`.
3. **Detail page** (`/books/[id]`) — one book. Link from the list.
4. **Change status** on the detail page (select or buttons). The list should show the new status when you go back.
5. Empty state when there are no books.
6. Seed 3 books so the first load is not blank (unless they use only `localStorage` — then document “click Reset seed”).

### Constraints

- No console errors on the happy path.
- Titles should not be empty strings after trim.
- `NOTES.md`: where data lives and how you would replace it with an API.

### Deliverables

- Runnable `npm`/`pnpm` app
- `NOTES.md`

### Submission

Repo or zip. Include Node version and the dev command.

---

## Stretch

Only if add/list/detail work:

- Filter by status on the list
- `localStorage` so refresh keeps books
- A disabled submit while saving (even if save is local)
