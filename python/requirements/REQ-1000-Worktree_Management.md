---
id: REQ-1000
title: Worktree Management
parent: none
level: L0
status: draft
source:
  - apps/server/src/services/worktree-metadata.ts
  - apps/server/src/lib/worktree-metadata.ts
  - apps/server/src/routes/worktree (all route handlers)
  - libs/git-utils/
depends_on: []
---

# REQ-1000 — Worktree Management

## Statement

Automaker must manage isolated git worktrees so that each agent run operates on a dedicated branch and directory, preventing AI agents from polluting the main working tree. The system creates worktrees on demand, tracks metadata about active worktrees, and cleans them up on success or abandonment. This is the load-bearing foundation of agent execution — nothing else ships without it.

## User-visible behavior

- When a user starts a feature, the server creates a new git worktree in a known location, checks out a feature-specific branch, and the agent run operates in that directory.
- The worktree's path, branch name, and status are visible in the UI's worktree panel.
- Successful completion or explicit abandonment removes the worktree and its branch per the JS behavior.
- Failures leave the worktree in place for inspection rather than silently deleting user work.

## Implementation notes (non-binding)

- CLI `git` via `subprocess` for worktree operations (`git worktree add`, `list`, `remove`). Avoid `pygit2` unless performance demands — worktree commands are low-frequency.
- `pathlib.Path` for path handling (Windows-safe).
- Worktree root under `.automaker/worktrees/<feature-id>/` by convention — verify against JS behavior.
- Cleanup must survive partial failure; idempotent delete.
- `psutil` for tree-kill of processes that might hold file locks on Windows before removal.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
