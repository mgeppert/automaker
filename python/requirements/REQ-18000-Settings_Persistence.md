---
id: REQ-18000
title: Settings Persistence
parent: none
level: L0
status: draft
source:
  - apps/server/src/lib/settings-helpers.ts
  - apps/server/src/lib/validation-storage.ts
  - apps/server/src/routes/ (settings handlers)
  - docs/settings-api-migration.md
  - docs/UNIFIED_API_KEY_PROFILES.md
depends_on: []
---

# REQ-18000 — Settings Persistence

## Statement

Automaker persists global settings in `data/settings.json` and per-project settings in `.automaker/settings.json`, with atomic writes, schema validation, and migration support. The schemas must match the JS versions exactly (Port Rule 3). Settings cover: user preferences, API key profiles, shortcuts, notification prefs, terminal configuration, theme, etc.

## User-visible behavior

- Settings UI loads, edits, and saves without loss.
- A user's existing `data/settings.json` from the JS version works unchanged when opened by the Python port.
- Concurrent edits (e.g. via multiple tabs) don't corrupt the file.

## Implementation notes (non-binding)

- `pydantic` for settings schemas; field-by-field parity with JS.
- Atomic writes: write temp file, fsync, rename.
- `portalocker` for cross-platform file locking during writes.
- Migrations: versioned schema; apply on load if old version detected. Match JS migration semantics.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
