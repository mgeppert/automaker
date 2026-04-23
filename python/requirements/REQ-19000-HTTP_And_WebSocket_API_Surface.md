---
id: REQ-19000
title: HTTP And WebSocket API Surface
parent: none
level: L0
status: draft
source:
  - apps/server/src/index.ts
  - apps/server/src/routes/ (all route handlers)
  - apps/server/src/lib/events.ts
  - apps/server/src/middleware/
depends_on:
  - REQ-17000
---

# REQ-19000 — HTTP And WebSocket API Surface

## Statement

The Python server exposes the HTTP REST endpoints and WebSocket event streams that the existing React UI expects. This is the wire contract and is part of the "must match" correctness oracle (Port Rule 2) — any response shape, status code, or event payload that diverges breaks the UI. All individual routes ultimately live under this Feature, even though most Features (e.g. Feature Management, Worktree, etc.) also own their subset of routes.

## User-visible behavior

- The UI, unchanged, works against the Python server exactly as it did against the JS server.
- Error responses have the same shape (status codes, JSON error envelope) as JS.
- WebSocket events (names, payloads, ordering) match JS so event handlers don't need to change.

## Implementation notes (non-binding)

- FastAPI for routing; `pydantic` for request/response models.
- WebSocket: FastAPI's `WebSocket` + an internal event bus so services emit events that are broadcast to connected clients.
- Middleware: CORS, auth enforcement, JSON content-type validation (see JS `middleware/` for the list).
- Generate an OpenAPI schema and diff it against a snapshot of JS routes as a CI check.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
