---
id: REQ-20000
title: Terminal PTY Integration
parent: none
level: L0
status: draft
source:
  - apps/server/src/services/terminal-service.ts
  - apps/server/src/lib/terminal-themes-data.ts
  - docs/terminal.md
  - docs/terminal-custom-configs-plan.md
depends_on:
  - REQ-19000
---

# REQ-20000 — Terminal PTY Integration

## Statement

Automaker embeds an interactive terminal in the UI (xterm.js on the client), backed by a real pseudo-terminal (PTY) on the server. The server spawns shells in user-chosen directories, relays stdin/stdout/stderr to the client over WebSocket, handles resize, and applies terminal themes. Must work on Windows and Linux.

## User-visible behavior

- Terminal tab in the UI functions as a real shell: commands run, output renders, resize reflows, themes apply.
- On Windows, ConPTY-backed shells work (Win10 1809+); user sees a clear error on older Windows.
- Terminal sessions survive across minor UI disconnects where JS preserves them.

## Implementation notes (non-binding)

- `ptyprocess` on Linux + `pywinpty` (ConPTY) on Windows behind a unified `PtyBackend` abstraction. This is the largest cross-platform concession in the port.
- Process spawning: pass argv lists (never strings); cross-platform env handling via `os.environ`.
- Resize: `ptyprocess.setwinsize()` / `pywinpty.setwinsize()`.
- Theme data: port JS theme data structure verbatim.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
