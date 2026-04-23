---
id: REQ-23000
title: MCP Integration
parent: none
level: L0
status: draft
source:
  - apps/server/src/services/mcp-test-service.ts
depends_on:
  - REQ-4000
---

# REQ-23000 — MCP Integration

## Statement

Automaker supports the Model Context Protocol (MCP), allowing users to connect MCP servers and have their tools available to agents. Includes MCP server configuration, connection testing, and tool registration with providers that support MCP.

## User-visible behavior

- User configures MCP servers in settings (command, args, env) with the same config shape as JS.
- User tests an MCP connection from the UI; success / failure surfaces clearly.
- Configured MCP tools are available to Claude (and other MCP-aware providers) during agent runs.

## Implementation notes (non-binding)

- Python MCP SDK exists; prefer it over hand-rolling the protocol.
- MCP server processes spawned via `asyncio.create_subprocess_exec`; stdio transport.
- Tool registration integrates with the Provider System (REQ-4000) tool-normalization layer.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
