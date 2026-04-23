---
id: REQ-22000
title: GitHub Integration
parent: none
level: L0
status: draft
source:
  - apps/server/src/services/github-pr-comment.service.ts
  - apps/server/src/services/cherry-pick-service.ts
  - apps/server/src/services/merge-service.ts
  - docs/pr-comment-fix-agent.md
  - docs/pr-comment-fix-prompt.md
  - docs/checkout-branch-pr.md
depends_on:
  - REQ-2000
---

# REQ-22000 — GitHub Integration

## Statement

Automaker integrates with GitHub for PR review workflows (fetching PR comments, feeding them to agents for automated resolution, posting replies), issue listing / conversion to features, and branch operations tied to PRs.

## User-visible behavior

- GitHub tab(s) show PRs and issues for the current repo.
- User can run "address PR comments" flow, which fires an agent on the comment threads.
- Issues can be converted into Kanban features.

## Implementation notes (non-binding)

- GitHub CLI (`gh`) via subprocess for operations where the CLI is already authenticated — matches JS approach.
- Direct GitHub REST via `httpx` for bulk queries where CLI is awkward.
- OAuth or PAT auth handled by the same credentials subsystem (REQ-17000).

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
