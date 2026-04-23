---
id: REQ-21000
title: Dev Server Integration
parent: none
level: L0
status: draft
source:
  - apps/server/src/services/dev-server-service.ts
  - docker-compose.dev-server.yml
depends_on:
  - REQ-19000
---

# REQ-21000 — Dev Server Integration

## Statement

Automaker can run a user-configured dev server command (e.g. `npm run dev`) as a managed subprocess per project, capture its logs, handle restart on demand, and surface status in the UI. This enables users to iterate on their app while Automaker agents modify its code.

## User-visible behavior

- User configures a dev server command in settings.
- Start / stop / restart controls in the UI work reliably; output streams to a log panel.
- Port conflicts and startup failures surface clear, actionable messages.

## Implementation notes (non-binding)

- `asyncio.create_subprocess_exec` for the dev process.
- Log capture via pipe reading; forward to WebSocket log stream.
- Process-tree kill on stop via `psutil` (child processes on Node dev servers are notoriously leaky otherwise).
- Port health check via `asyncio.open_connection` to `localhost:<port>`.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
