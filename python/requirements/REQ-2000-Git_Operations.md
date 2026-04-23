---
id: REQ-2000
title: Git Operations
parent: none
level: L0
status: draft
source:
  - apps/server/src/lib/git.ts
  - apps/server/src/lib/git-log-parser.ts
  - apps/server/src/services/branch-commit-log-service.ts
  - apps/server/src/services/branch-sync-service.ts
  - apps/server/src/services/branch-utils.ts
  - apps/server/src/services/checkout-branch-service.ts
  - apps/server/src/services/cherry-pick-service.ts
  - apps/server/src/services/commit-log-service.ts
  - apps/server/src/services/merge-service.ts
  - libs/git-utils/
depends_on: []
---

# REQ-2000 — Git Operations

## Statement

Automaker must perform git operations — branch creation and deletion, commit log retrieval, diff generation, checkout, cherry-pick, merge, remote sync — on behalf of the user and the agent execution system. This is a foundational subsystem used throughout: `execGitCommand` is a top-5 graph hub. Operations must work on Windows and Linux with cross-platform line-ending handling.

## User-visible behavior

- Commit log visible per-branch in the UI with the same fields the JS version provides.
- Diff views render file-by-file diffs identical to the JS behavior.
- Branch operations (create, delete, checkout) succeed silently or fail with actionable error messages.
- Cherry-pick and merge surface conflict information to the user the same way JS does.

## Implementation notes (non-binding)

- CLI `git` via `subprocess.run`/`asyncio.create_subprocess_exec`, not `pygit2`, for transparency and behavior parity.
- Parse git output carefully — porcelain formats are stable; ad-hoc output is not. Prefer `--porcelain` / `-z` where available.
- Windows: CRLF handling; avoid shell interpretation (`shell=False`, pass argv list).
- Consider a thin `GitRepo` class as the one place subprocess is invoked — everywhere else calls methods on it.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
