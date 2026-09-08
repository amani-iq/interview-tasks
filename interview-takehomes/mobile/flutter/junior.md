# Mobile / Flutter — Junior take-home

## Snapshot

| Field | Value |
| --- | --- |
| Track | Mobile |
| Stack | Flutter, Dart |
| Time box | 3–4 hours. Stop when the time is up. |
| Product | **Northline Errands** — simple todo list |
| Submit | Repo or zip + `NOTES.md` + how to run |

## Candidate brief

You are building **Northline Errands**, a phone app for a short shopping/todo list.

An item has `title` and `done`. No backend.

This is a take-home. Make the main loop work on a phone-sized screen.

### Time box

3–4 hours. Adding and ticking items matters more than animations.

### Rules of the exercise

- Flutter (latest stable is fine).
- `setState` is acceptable. Riverpod/Provider is fine if you already use it.
- Do not add Firebase.

### Requirements

1. **Home** — list of errands. Tapping the row or checkbox toggles `done`. Done items look different (strike-through or color).
2. **Add** — text field + button (or a second screen). Title required after trim. Empty submit shows an error, does not add a blank row.
3. **Delete** — swipe or an icon. Confirm is optional.
4. At least 3 seeded items on first run.
5. Must not overflow on a ~360dp wide screen with a long title.
6. Keyboard: you can still tap Add while the keyboard is open (or the field scrolls into view).

### Constraints

- One or two screens is enough.
- `NOTES.md`: Flutter version, device you used, and how state is stored (memory vs persist).

### Deliverables

- Flutter project that runs on simulator, emulator, or Chrome
- `NOTES.md`

### Submission

Repo or zip. Include `flutter --version` and how you launched it.

---

## Stretch

Only if add/toggle/delete work:

- Persist with `shared_preferences` (survive restart)
- Filter: all / open / done
- Extract an `Errand` model and a list widget
