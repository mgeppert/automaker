---
id: REQ-9000
title: Gemini Provider
parent: none
level: L0
status: draft
source:
  - apps/server/src/providers/gemini-provider.ts
  - apps/server/src/services/gemini-usage-service.ts
depends_on:
  - REQ-3000
  - REQ-4000
---

# REQ-9000 — Gemini Provider

## Statement

Automaker integrates with Google Gemini as an agent provider, including auth, model selection, agent runs, and usage tracking.

## User-visible behavior

- User configures a Google API key for Gemini.
- User picks a Gemini model; agent runs produce standard events.
- Usage tracking visible via the usage popover matching JS behavior.

## Implementation notes (non-binding)

- Google's `google-genai` Python SDK for Gemini access.
- Streaming via the SDK's async generator.
- Usage format per Port Rule 3.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
