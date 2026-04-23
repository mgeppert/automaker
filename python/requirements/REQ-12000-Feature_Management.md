---
id: REQ-12000
title: Feature Management
parent: none
level: L0
status: draft
source:
  - apps/server/src/services/feature-loader.ts
  - apps/server/src/services/feature-state-manager.ts
  - apps/server/src/services/feature-export-service.ts
  - apps/server/src/routes/features (all route handlers)
depends_on:
  - REQ-18000
---

# REQ-12000 — Feature Management

## Statement

Automaker manages "features" (work items on the Kanban board) including CRUD operations, Kanban state machine transitions, JSON persistence under `.automaker/features/<feature-id>/`, image attachments, import/export, and validation. Features are the primary user-facing unit of work.

## User-visible behavior

- Kanban board shows features grouped by status (backlog, in-progress, completed, etc.).
- User creates, edits, deletes, drags between columns, attaches images to features.
- Feature JSON persists at `.automaker/features/<id>/feature.json` with the same schema JS uses (Port Rule 3).
- Export produces a user-usable archive matching JS format.

## Implementation notes (non-binding)

- `pydantic` models for Feature; schema must match JS JSON shape.
- Atomic JSON writes via temp-file-then-rename pattern. `portalocker` for file locking when multiple processes might touch the same feature.
- Image handling via `Pillow` if processing is needed; passthrough otherwise.
- State machine validation: prevent invalid transitions (e.g. can't move from completed back to backlog without explicit reset, matching JS).

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
