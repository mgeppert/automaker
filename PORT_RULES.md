# Port Rules (JS → Python)

Durable constraints for porting `automaker/` (JS/TS) to `automaker/python/` (Python). These govern correctness, structure, and maintenance decisions throughout the port.

This file lives on the `python-port` branch only. `main` tracks upstream (`AutoMaker-Org/automaker`) and is never modified beyond merges from upstream.

## Remotes

- `origin` — `github.com/mgeppert/automaker` — our fork, primary push destination.
- `upstream` — `github.com/AutoMaker-Org/automaker` — read-only. Pull upstream updates with `git fetch upstream && git merge upstream/main`. The push URL is intentionally set to an invalid value.
- `gitea` — `gitea.mgeppert.com:2222/mgeppert/AngeticCoding.git` — second push destination (local NAS).

Push sequence when publishing work on this branch:

```
git push origin python-port
git push gitea python-port
```

## Rules

**1. Web-only, Windows + Linux.**
No Electron desktop build. The port must run on Windows and Linux (dev machine is CachyOS). Prefer cross-platform choices; flag anything Unix-only early — pty libraries, signal handling, fork semantics, process-tree kill, file locking. Desktop packaging may be revisited later.

**2. Correctness oracle = user-visible behavior.**
**Must match** the JS original: UI flows, error messages (by *meaning*, not exact wording), the HTTP + WebSocket wire contract, and observable outcomes (files written under `.automaker/`, worktrees created, branches named, PR comments posted, etc.). **Free to redesign:** internal service decomposition, library/framework choices, async model, log formats, internal IDs, class names, DI patterns, error-class taxonomies.

**3. Config file formats stay compatible where practical.**
User-facing files under `.automaker/` and `data/` — settings, credentials, features, context, sessions — keep their schema and field names. Default tolerance: "same schema, small serialization differences OK" (e.g. date formats). Tighten to "bit-compatible" for files a user might realistically share between JS and Python runs (credentials especially). Call out deliberate divergences in the requirement that introduces them.

**4. Macro directory layout mirrors the original.**
`python/` parallels `apps/server/src/*` and `libs/*` at the folder level, so upstream JS changes map to obvious Python locations. TS hyphen-case → Python snake_case is expected and not a divergence. Inside a module, internal organization is free. When a JS file's scope would idiomatically split into multiple Python modules, document the 1-to-N mapping in the module header.

**5. Requirements are singular and diagnostic.**
Each requirement has a single pass/fail test that, on failure, points at one place to fix. Governing question: **"If this test goes red, is there one place in the code to look?"** Requirements form a tree; parent *Features* exist for grouping and progress rollup; only leaves are tested. Split rather than bundle when in doubt. Tests are tagged with requirement IDs so CI output names exactly what broke.

## Adds beyond parity

- **Startup dependency check** (`automaker-py --check` / `doctor` subcommand): verifies Python version, git version, required packages, optional provider CLIs, writable data/project dirs, ConPTY availability on Windows.
- **Help utilities** and clear config-file defaults.
- **Mock provider mode** (parity with `AUTOMAKER_MOCK_AGENT=true`) so CI and dev loops don't burn API credits.
- **Cross-platform CI** from day one: GitHub Actions running the full test suite on both Windows and Linux runners.
- **Structured logging + request IDs** scaffolded before any feature work.
