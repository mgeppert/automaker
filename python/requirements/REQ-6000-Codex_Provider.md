---
id: REQ-6000
title: Codex Provider
parent: none
level: L0
status: draft
source:
  - apps/server/src/providers/codex-provider.ts
  - apps/server/src/providers/codex-config-manager.ts
  - apps/server/src/providers/codex-models.ts
  - apps/server/src/providers/codex-sdk-client.ts
  - apps/server/src/providers/codex-tool-mapping.ts
  - apps/server/src/services/codex-app-server-service.ts
  - apps/server/src/services/codex-model-cache-service.ts
  - apps/server/src/services/codex-usage-service.ts
  - apps/server/src/lib/codex-auth.ts
depends_on:
  - REQ-3000
  - REQ-4000
---

# REQ-6000 — Codex Provider

## Statement

Automaker integrates with OpenAI Codex, including agent runs, config management, model cache, TOML-based config file handling, auth flow, and usage tracking. Codex has its own SDK/CLI and app-server model (see JS `codex-app-server-service.ts`) — port covers the same surface area.

## User-visible behavior

- User can configure Codex credentials and select a Codex model.
- Codex-specific config files persist in the expected location with the expected TOML shape.
- Agent runs against Codex behave identically (from the user's view) to Claude runs.

## Implementation notes (non-binding)

- TOML read/write via stdlib `tomllib` (read) + `tomli-w` (write). JS uses its own TOML formatter; match output shape on round-trip.
- Codex SDK: Python equivalent TBD — may be CLI-spawning if no first-party Python SDK.
- Usage tracking file compatible with JS per Port Rule 3.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
