---
id: REQ-5000
title: Claude Provider
parent: none
level: L0
status: draft
source:
  - apps/server/src/providers/claude-provider.ts
  - apps/server/src/services/claude-usage-service.ts
  - apps/server/src/lib/sdk-options.ts
  - apps/server/src/lib/enhancement-prompts.ts
depends_on:
  - REQ-3000
  - REQ-4000
---

# REQ-5000 — Claude Provider

## Statement

Automaker integrates with Anthropic's Claude via the Claude Agent SDK (Python), supporting agent runs with tool use, permission flow, session management, model selection (haiku/sonnet/opus aliases), and usage tracking. Claude is the primary and most-tested provider; other providers follow the pattern established here.

## User-visible behavior

- User configures an Anthropic API key (or uses Claude Code CLI auth, same as JS behavior).
- User selects a Claude model alias in the feature UI; alias resolves to a concrete model ID.
- Agent responses stream to the UI token-by-token.
- Tool use and permission prompts surface the same events JS does.
- Usage (input/output tokens, cost estimate) visible per session in the usage popover.

## Implementation notes (non-binding)

- `claude-agent-sdk` for Python (verify version parity with JS Agent SDK features we depend on — this is the highest-risk unknown and should be poked at early).
- Model alias resolution reuses logic from REQ-4000's model-resolver port.
- Streaming via the SDK's async iterator; forward each chunk to the WebSocket.
- Usage tracking writes to `data/` files compatible with JS usage format per Port Rule 3.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
