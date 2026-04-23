---
id: REQ-13000
title: Pipeline Orchestration
parent: none
level: L0
status: draft
source:
  - apps/server/src/services/pipeline-orchestrator.ts
  - apps/server/src/services/pipeline-service.ts
  - apps/server/src/services/auto-loop-coordinator.ts
  - apps/server/src/services/execution-service.ts
depends_on:
  - REQ-3000
  - REQ-12000
---

# REQ-13000 — Pipeline Orchestration

## Statement

Automaker supports multi-step pipelines (e.g. plan → execute → review → commit) and an auto-mode that advances features through stages automatically without user intervention. Pipelines wrap agent runs with transition logic, step-specific prompts, and state advancement.

## User-visible behavior

- User configures pipeline steps per feature or globally.
- Auto-mode button advances features through pipeline stages; user can pause and resume.
- Pipeline step status visible in the UI with clear progress indication.

## Implementation notes (non-binding)

- State machine pattern; `pydantic` models for pipeline definitions.
- Auto-mode is a long-running `asyncio` task per feature with graceful cancellation.
- Step definitions loaded from configuration (global and per-project).

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
