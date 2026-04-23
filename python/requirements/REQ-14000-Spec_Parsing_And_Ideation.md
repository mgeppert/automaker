---
id: REQ-14000
title: Spec Parsing And Ideation
parent: none
level: L0
status: draft
source:
  - libs/spec-parser/
  - apps/server/src/services/ideation-service.ts
  - apps/server/src/lib/app-spec-format.ts
  - docs/prd-to-features-guide.md
depends_on:
  - REQ-5000
---

# REQ-14000 — Spec Parsing And Ideation

## Statement

Automaker parses user-provided `.automaker/spec.md` project specifications into structured feature lists, and provides an ideation service that uses an AI provider to generate feature suggestions from the spec. The parser's output shape and ideation workflow must match JS user expectations.

## User-visible behavior

- User writes `.automaker/spec.md` in a supported format; the parser extracts features and presents them in the ideation/add-feature UI.
- User runs ideation on a spec; AI-generated feature suggestions appear in the UI identical to JS layout.
- Import of generated features into the Kanban board matches JS flow.

## Implementation notes (non-binding)

- Markdown parsing: `markdown-it-py` or `mistune`; the JS uses its own parser, so match output shape rather than implementation.
- Ideation calls out to the configured provider (REQ-5000 or similar).
- `pydantic` for the parsed spec data model.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
