# Mobile / Flutter — Mid take-home

## Snapshot

| Field | Value |
| --- | --- |
| Track | Mobile |
| Stack | Flutter, Dart |
| Time box | 4–6 hours. Stop when the time is up. |
| Product | **Northline Pocket** — field checklist |
| Submit | Repo or zip + `NOTES.md` + how to run |

## Candidate brief

You are building **Northline Pocket**, a phone app for a field tech.

Each job is a checklist. The tech opens a job, ticks items, adds a note, and marks the job done. There is no backend. Data must survive app restart.

### Time box

4–6 hours. A reliable job loop beats animations and extra screens.

### Rules of the exercise

- Flutter (latest stable is fine).
- State: you may use built-ins, Riverpod, Bloc, or Provider. Use one on purpose.
- Local store: `shared_preferences` is acceptable for a thin slice; `drift` / `hive` / `sqflite` is better if you have time. Say why.
- Do not add Firebase unless you truly need it (you do not).

### Requirements

1. **Job list** — seeded jobs (at least 4) with title, site name, and progress (`3/8`).
2. **Job detail** — checklist items, each with `label` and `done`. Tapping toggles. Progress on the list updates when you go back.
3. **Add note** on a job (plain text, max 200 chars). Persist it.
4. **Complete job** — only if every item is done. Completed jobs stay on the list, visually distinct, not editable.
5. Data survives process death (fully quit and reopen).
6. Empty / first-run: if they reset storage, show a useful empty state and a way to reseed (button is fine).
7. Layout must work at a phone width (~360dp) and not overflow a long item label.

### Constraints

- Separate “what the job is” from “how it is drawn”. One giant build method is a smell.
- No overflow in debug on the seeded data.
- `NOTES.md` must say how state is lifted and how persistence is tested (even if you tested by hand).

### Deliverables

- Flutter project that runs on iOS simulator, Android emulator, or Chrome
- Seed + persist
- `NOTES.md`: state choice, persistence choice, what you would sync later

### Submission

Repo or zip. Include Flutter version (`flutter --version`) and the device you used.

---

## Stretch

Only if the core is solid:

- Undo a toggle (snackbar)
- Search / filter jobs
- Simple widget or golden test on the complete-job rule
- Dark mode that still keeps completed vs open obvious
