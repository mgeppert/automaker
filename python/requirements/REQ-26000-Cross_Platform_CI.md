---
id: REQ-26000
title: Cross Platform CI
parent: none
level: L0
status: draft
source:
  - .github/workflows/ (existing JS CI — for reference)
  - (net-new Python CI workflow)
depends_on:
  - REQ-11000
---

# REQ-26000 — Cross Platform CI

## Statement

**Net-new capability for the Python port.** A GitHub Actions workflow runs the full Python test suite on both Windows and Linux runners for every PR and every push to the `python-port` branch. Coverage and lint gates configurable.

## User-visible behavior

- PR pages on GitHub show CI status for Windows and Linux runs separately.
- Test failures on either OS block merge (if branch protection rules are enabled).
- Coverage report visible as a PR comment or check annotation.

## Implementation notes (non-binding)

- `.github/workflows/python-ci.yml` with `matrix: os: [ubuntu-latest, windows-latest]`.
- `uv` for fast dependency install, or `pip + pip-tools`.
- Use the Mock Provider (REQ-11000) so CI doesn't need API keys.
- Cache pip / uv downloads per OS.
- Consider adding a ruff lint + mypy type-check gate in the same workflow.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
