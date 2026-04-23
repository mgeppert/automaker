---
id: REQ-10000
title: OpenCode Provider
parent: none
level: L0
status: draft
source:
  - apps/server/src/providers/opencode-provider.ts
  - OPENCODE_CONFIG_CONTENT
depends_on:
  - REQ-3000
  - REQ-4000
---

# REQ-10000 — OpenCode Provider

## Statement

Automaker integrates with OpenCode as an agent provider, invoked via its CLI and configured via an OpenCode-specific config file.

## User-visible behavior

- User installs OpenCode CLI; Automaker detects it and makes it available as a provider.
- Agent runs via OpenCode stream events the same as other providers.

## Implementation notes (non-binding)

- CLI-spawning provider. Detect presence of `opencode` binary on PATH (with common fallback locations per JS).
- Config file content matches JS `OPENCODE_CONFIG_CONTENT` on disk.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
