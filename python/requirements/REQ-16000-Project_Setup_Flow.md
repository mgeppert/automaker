---
id: REQ-16000
title: Project Setup Flow
parent: none
level: L0
status: draft
source:
  - apps/server/src/routes/setup/ (createSetupRoutes and nested route handlers)
  - apps/server/src/services/init-script-service.ts
  - docs/worktree-init-script-example.sh
depends_on:
  - REQ-17000
  - REQ-18000
---

# REQ-16000 — Project Setup Flow

## Statement

Automaker provides a first-run setup flow for new projects: creates the `.automaker/` directory skeleton, prompts the user for provider configuration and API keys, establishes workspace defaults, and optionally runs a project-specific init script. `createSetupRoutes` is a god node (#4) — the flow is touched from many places.

## User-visible behavior

- User opens a fresh project directory; the UI guides them through setup.
- Setup collects: provider choice, credentials, workspace settings, optional init script.
- On completion, `.automaker/` is initialized and the project is ready for feature work.
- Re-running setup on an existing project updates rather than wipes.

## Implementation notes (non-binding)

- Multiple routes for each setup step; shared state via a setup-session model.
- Credential storage via REQ-17000.
- Init script execution via `subprocess` — sandbox assumptions match JS (e.g. cwd, env).

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
