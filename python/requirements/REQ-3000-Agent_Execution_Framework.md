---
id: REQ-3000
title: Agent Execution Framework
parent: none
level: L0
status: draft
source:
  - apps/server/src/services/agent-executor.ts
  - apps/server/src/services/agent-executor-types.ts
  - apps/server/src/services/agent-service.ts
  - apps/server/src/services/execution-service.ts
  - apps/server/src/services/execution-types.ts
  - apps/server/src/services/concurrency-manager.ts
  - apps/server/src/services/event-history-service.ts
depends_on:
  - REQ-1000
  - REQ-2000
  - REQ-4000
---

# REQ-3000 — Agent Execution Framework

## Statement

Automaker must run AI agents against features in a uniform framework that handles lifecycle (init / stream / permission-request / complete / cleanup), event streaming to the UI, permission enforcement, concurrency limits, session persistence, and error classification. This framework is provider-agnostic — it delegates to whichever provider (Claude, Codex, Cursor, etc.) is configured, but the orchestration around the provider call is shared.

## User-visible behavior

- Starting a feature produces a stream of events to the UI (agent output, tool calls, permission prompts, progress updates, completion).
- Permission requests block until the user approves or rejects, matching the JS UX.
- Errors during execution surface as classified, actionable messages rather than raw stack traces.
- Session history persists so a user can review what the agent did after the fact.

## Implementation notes (non-binding)

- `asyncio` throughout — agent runs are long-lived I/O-bound workloads.
- FastAPI `WebSocket` for event streaming, `pydantic` models for event shapes.
- Concurrency: `asyncio.Semaphore` per-provider, global cap configurable.
- Event history to JSON files under `data/agent-sessions/` matching JS layout (see Port Rule 3 — config compatibility).

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
