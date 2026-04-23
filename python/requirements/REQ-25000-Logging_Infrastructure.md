---
id: REQ-25000
title: Logging Infrastructure
parent: none
level: L0
status: draft
source:
  - libs/utils/ (createLogger)
  - various services calling createLogger
depends_on: []
---

# REQ-25000 — Logging Infrastructure

## Statement

Automaker's Python server uses structured logging with per-request correlation IDs, configurable log levels, file rotation, and separate streams for app logs versus agent logs. Log format is consistent across all subsystems. This is scaffolded before feature code so every requirement can assume it exists.

## User-visible behavior

- Logs are readable in dev (pretty-printed, colorized).
- Logs are queryable in production (structured JSON).
- A user reporting a bug can be asked for a request ID and we can reconstruct their session.
- Log file rotation prevents unbounded disk consumption.

## Implementation notes (non-binding)

- `structlog` for structured logging with both dev and production renderers.
- Per-request correlation ID via a FastAPI middleware injecting a context var.
- File rotation via `logging.handlers.TimedRotatingFileHandler` or `loguru` if we switch.
- Keep log output of agent runs (potentially huge) on a separate logger than app logs so verbosity can be tuned independently.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
