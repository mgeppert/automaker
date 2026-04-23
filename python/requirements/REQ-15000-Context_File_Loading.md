---
id: REQ-15000
title: Context File Loading
parent: none
level: L0
status: draft
source:
  - libs/utils/ (context file loader — loadContextFiles)
  - apps/server/src/lib/enhancement-prompts.ts
  - docs/context-files-pattern.md
depends_on: []
---

# REQ-15000 — Context File Loading

## Statement

Automaker loads markdown files from `.automaker/context/` and optional project-level `CLAUDE.md` / context files into agent prompts, so project-specific rules and information are available to AI agents at run time. Parity with the JS `loadContextFiles` utility.

## User-visible behavior

- User drops markdown files into `.automaker/context/`; the next agent run picks them up with no other action.
- Context file contents appear in agent system prompts in the same order and format as JS.
- Context visibility / debug view in the UI shows what's being injected.

## Implementation notes (non-binding)

- Pure file I/O + string concatenation; no LLM involved.
- Respect the same file-ordering and delimiter conventions as JS.
- Directory watching optional; reload-on-each-run is fine if JS does the same.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
