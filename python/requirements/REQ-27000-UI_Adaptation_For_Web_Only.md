---
id: REQ-27000
title: UI Adaptation For Web Only
parent: none
level: L0
status: draft
source:
  - apps/ui/src/electron/ (all files — to be audited)
  - apps/ui/src/lib/electron.ts
  - apps/ui/ (all files referencing window.electron)
depends_on: []
---

# REQ-27000 — UI Adaptation For Web Only

## Statement

The existing React UI in `apps/ui/` was built to run in both Electron and browser modes. For the Python port we are dropping Electron (Port Rule 1), so every UI call site that gates on `window.electron?` or imports from `src/electron/` must have a web-only path, or be removed if Electron-exclusive. `getElectronAPI()` is a top-10 graph hub, so this is non-trivial and deserves an explicit Feature rather than being hidden inside another.

## User-visible behavior

- The UI works fully in a plain browser against the Python server — no broken buttons, no missing features that are supposed to be available in web mode.
- Features that were Electron-only (e.g. native file dialog invoked from main process) either gain a web equivalent (browser file picker) or are clearly removed / disabled with user-visible messaging.

## Implementation notes (non-binding)

- This is a **TypeScript/React change**, not Python. It's a port requirement because the Python port isn't usable without it, not because it's Python work.
- Audit via grep for `window.electron`, `getElectronAPI`, imports from `@/electron/*`, and the `src/electron/` directory itself.
- Categorize each hit: (a) already has a web fallback — verify; (b) missing a web fallback — add one; (c) Electron-only feature — remove / disable.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
