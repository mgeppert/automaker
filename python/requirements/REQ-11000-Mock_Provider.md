---
id: REQ-11000
title: Mock Provider
parent: none
level: L0
status: draft
source:
  - apps/server/src/providers/mock-provider.ts
depends_on:
  - REQ-3000
  - REQ-4000
---

# REQ-11000 — Mock Provider

## Statement

Automaker supports a Mock provider that returns canned responses without calling any real AI backend. Enables CI, development loops, and E2E testing without burning API credits or depending on network. Activation mirrors JS: `AUTOMAKER_MOCK_AGENT=true` env var.

## User-visible behavior

- When mock mode is active, the UI shows a clear indicator (matches JS visual cue).
- Agent runs produce scripted event sequences that exercise the UI's event handling.
- Timing is fast — no real API latency.

## Implementation notes (non-binding)

- Pure Python; no external SDK.
- Scripted sequences loaded from fixture files so tests can parametrize over them.
- Respects the same provider interface (REQ-4000) as real providers — indistinguishable from the framework's perspective.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
