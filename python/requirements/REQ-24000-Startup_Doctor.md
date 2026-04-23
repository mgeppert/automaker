---
id: REQ-24000
title: Startup Doctor
parent: none
level: L0
status: draft
source:
  - (net-new; no direct JS equivalent)
depends_on: []
---

# REQ-24000 — Startup Doctor

## Statement

**Net-new capability, not in the JS original.** Automaker runs a dependency check at server startup and on demand via an `automaker-py --check` (or `doctor`) subcommand. Verifies Python version, git binary and version, required Python packages importable, optional provider CLIs (claude, codex, etc.), writable data/project directories, ConPTY availability on Windows if terminal is enabled. Emits pass/fail per check with actionable diagnostic messages.

## User-visible behavior

- At startup, doctor runs silently if all checks pass, or prints a clearly formatted list of failures with suggested fixes.
- `automaker-py --check` runs doctor on demand and exits 0 on success, non-zero on any failure.
- Optional checks (provider CLIs, terminal) emit warnings rather than errors — only truly required dependencies block startup.

## Implementation notes (non-binding)

- Check implementations pure-Python, each returning a structured result (`Passed`, `Warning`, `Failed` with message).
- Output format: human-readable with colors when TTY, plain-text when piped, structured JSON with `--json` flag.
- `rich` or `click` for formatting.
- Each check cheap to run (<100ms typical); overall doctor <1s.

## Test plan

(To be written during decomposition; leaves carry tests, not L0.)

## Children

(To be populated during L1 decomposition.)
