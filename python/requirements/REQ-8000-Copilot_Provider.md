---
id: REQ-8000
title: Copilot Provider
parent: none
level: L0
status: draft
source:
  - apps/server/src/providers/copilot-provider.ts
  - apps/server/src/services/copilot-connection-service.ts
depends_on:
  - REQ-3000
  - REQ-4000
---

# REQ-8000 — Copilot Provider

## Statement

Automaker integrates with GitHub Copilot as an agent provider, including Copilot's connection/auth flow and its specific agent invocation semantics.

## User-visible behavior

- User configures Copilot auth via GitHub (same flow as JS).
- Agent runs against Copilot produce events identical to other providers from the user's view.

## Implementation notes (non-binding)

- GitHub Copilot SDK access is via Copilot's HTTP API + auth token. `httpx` for HTTP, `pydantic` for request/response shapes.
- Connection state tracked per-session.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
