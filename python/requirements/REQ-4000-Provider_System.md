---
id: REQ-4000
title: Provider System
parent: none
level: L0
status: draft
source:
  - apps/server/src/providers/base-provider.ts
  - apps/server/src/providers/provider-factory.ts
  - apps/server/src/providers/types.ts
  - apps/server/src/providers/cli-provider.ts
  - apps/server/src/providers/index.ts
  - apps/server/src/providers/tool-normalization.ts
  - apps/server/src/providers/simple-query-service.ts
depends_on: []
---

# REQ-4000 — Provider System

## Statement

Automaker supports multiple AI providers (Claude, Codex, Cursor, Copilot, Gemini, OpenCode, Mock). This requirement covers the abstraction layer: a common provider interface, registration/discovery mechanism, factory that picks the right provider based on configuration, and tool-call normalization across providers that expose different tool schemas. Individual providers are their own L0 Features (REQ-5000 through REQ-11000); this one is the shared spine.

## User-visible behavior

- User selects a provider in settings; the UI shows available providers and which are configured.
- User switches providers per-feature without restarting the server.
- Provider-specific capabilities (model list, supported tools) surface in the UI identically to the JS version.

## Implementation notes (non-binding)

- `Protocol` or `ABC` for the provider interface — `pydantic.BaseModel` for shared config shapes.
- Registry pattern: each provider module registers itself on import; factory resolves by name.
- Tool normalization: translate between provider-specific tool schemas and an internal canonical form (same as JS `tool-normalization.ts`).
- CLI-spawning providers share a base class (mirror of JS `cli-provider.ts`) for subprocess management, auth detection, CLI version checks.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
