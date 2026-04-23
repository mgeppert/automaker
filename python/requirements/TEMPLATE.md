---
id: REQ-XXXX
title: <short human-readable title>
parent: none
level: L0
status: draft
source:
  - <file path>::<function or class>
depends_on: []
---

# REQ-XXXX — <Title>

## Statement

<Plain-language description of what must be true. For leaves, this is a single testable claim. For parents, this is a fuzzy Feature statement that will be decomposed in later passes.>

## User-visible behavior

<What the user sees, touches, or observes. This is the part that MUST match the JS original per Port Rule 2. For parents, summarize the user-facing surface of the whole subsystem.>

## Implementation notes (non-binding)

<Python library candidates (see PORT_RULES.md Ground Rules for defaults), design hints, Pythonic divergences from the JS implementation. This section is NOT part of the correctness oracle — it's guidance only and free to ignore later.>

## Test plan

<For leaves: one pytest test case per singular assertion. Each entry gives a pytest function name and a 1-3 line description of what the test asserts.

For parents: leave blank; leaves carry the tests.>

- `test_REQ_<id>_<suffix>`: <one-line description of what this test asserts>

## Children

<For parents: list of child REQ IDs this decomposes into.
For leaves: "none".>

- none
