---
id: REQ-17000
title: Authentication And Credentials
parent: none
level: L0
status: draft
source:
  - apps/server/src/lib/auth.ts
  - apps/server/src/lib/auth-utils.ts
  - apps/server/src/middleware/ (auth middleware)
  - apps/server/src/routes/setup/ (credentials handlers)
depends_on:
  - REQ-18000
---

# REQ-17000 — Authentication And Credentials

## Statement

Automaker authenticates UI sessions and stores provider credentials (API keys, tokens). Handles session token issuance for WebSocket connections, session expiration, credential persistence in `data/credentials.json`, and per-provider auth detection (e.g. "is Claude CLI logged in").

## User-visible behavior

- Login screen (if auth is enabled per config) accepts user credentials.
- Provider credentials persist across restarts in the same file shape as JS (Port Rule 3 — likely tightened to bit-compatible here so users don't have to re-auth).
- Session tokens are issued per connection and time out per JS behavior.

## Implementation notes (non-binding)

- FastAPI dependencies for route-level auth enforcement.
- Session tokens via signed JWTs (`python-jose` or `authlib`) or simple signed cookies — match JS token format if the UI caches tokens.
- Credentials file: JSON, schema-compatible with JS per Port Rule 3.
- Consider OS keyring integration later; JSON file parity first.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
