---
id: REQ-7000
title: Cursor Provider
parent: none
level: L0
status: draft
source:
  - apps/server/src/providers/cursor-provider.ts
  - apps/server/src/providers/cursor-config-manager.ts
  - apps/server/src/services/cursor-config-service.ts
  - scripts/get-cursor-token.sh
  - docs/add-new-cursor-model.md
depends_on:
  - REQ-3000
  - REQ-4000
---

# REQ-7000 — Cursor Provider

## Statement

Automaker integrates with Cursor's agent capabilities via Cursor's config and auth mechanisms. Port covers provider implementation, Cursor-specific config management, and the auth token flow that JS handles via a shell script.

## User-visible behavior

- User configures Cursor auth (JS uses a helper shell script — the Python port replaces that with a built-in flow where practical).
- User selects Cursor models; the list matches Cursor's available models.
- Agent runs via Cursor stream to the UI the same as any other provider.

## Implementation notes (non-binding)

- CLI-spawning provider (mirrors JS pattern). `subprocess` with argv.
- Windows: watch for shell-specific auth commands that don't port directly.
- Config files under user's Cursor config dir — path discovery via `platformdirs` for cross-platform.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
