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

## Ground Rules

Rules governing **how** the port is planned and built (distinct from the substantive rules above which govern **what** the port must produce).

### Library-first ("don't reinvent the wheel")

Prefer mature Python libraries over hand-rolled equivalents. Every implementation requirement must list its candidate Python libraries in the Implementation notes section and justify the choice. "No library; hand-rolled" is allowed but requires a one-sentence reason.

Default picks (use unless there's a real reason not to):

| Concern | Library |
|---|---|
| HTTP server + routing | `fastapi` + `uvicorn` |
| Data validation & settings | `pydantic` (v2) + `pydantic-settings` |
| HTTP client (sync + async) | `httpx` |
| Logging | `structlog` |
| Terminal (PTY), cross-platform | `ptyprocess` (Linux) + `pywinpty` (Windows) behind one abstraction |
| Process utilities (kill tree, signals) | `psutil` |
| Git operations | `subprocess` (CLI `git`) — use `pygit2` only if performance requires |
| Testing | `pytest` + `pytest-asyncio` + `pytest-cov` |
| TOML / YAML | stdlib `tomllib` / `pyyaml` |
| File locking | `portalocker` |

### Multi-pass requirements process

Requirements are written iteratively:

1. **Pass 1 (L0):** coarse Feature-level statements. Not singular, not testable. Big buckets. Expect ~15–25 L0 requirements.
2. **Pass 2+ (L1, L2, ...):** decompose each leaf until it is singular and diagnostic per Rule 5.
3. Only leaves are implemented and tested. Parent Features are grouping + progress rollup only.

### Requirement IDs and traceability

IDs are `REQ-<hierarchy>` with dotted hierarchical segments at 1000-step spacing:

- L0 Features: `REQ-1000`, `REQ-2000`, `REQ-3000`, ...
- L1: `REQ-1000.1000`, `REQ-1000.2000`, ...
- L2: `REQ-1000.1000.1000`, ...

The `REQ-` prefix makes them grep-able. The 1000-step spacing leaves room to insert siblings without renumbering.

Every requirement carries **two traceability axes**:

- **Vertical** (parent → child in our doc): encoded in the hierarchical ID.
- **Horizontal** (to the JS original): a `source:` frontmatter field naming file paths and functions in `automaker/` that the requirement describes. Example: `apps/server/src/services/agent-executor.ts::AgentExecutor.execute()`.

Requirements may also carry `depends_on: [REQ-..., ...]` to make implementation ordering explicit.

### Test plan on every leaf

Every leaf (testable) requirement has a **Test plan** section with a brief description (1–3 lines per test case) of what pytest tests will verify it. This is the canonical description of the test and lives in the same file as the requirement so the two can't drift. An optional `TESTS.md` rollup can be generated from the per-requirement Test plans once we have enough requirements to justify it.

### Testing conventions

- **Framework:** `pytest` with `pytest-asyncio` for async tests and `pytest-cov` for coverage.
- **Function naming:** `def test_REQ_<id_with_underscores_for_dots>_<descriptive_suffix>():` — e.g. `test_REQ_1000_1000_worktree_created_in_automaker_dir`. CI failure output names the broken requirement directly.
- **Marker:** every test has exactly one `@pytest.mark.req("REQ-1000.1000")` marker. Marker is registered in `conftest.py`. Enables:
  - Running tests for a specific requirement: `pytest -m 'req("REQ-1000.1000")'`.
  - Mechanical generation of the requirement → test traceability matrix.
  - A CI check enforcing "every test has exactly one `req` marker."

### Context management and handoff

Long-running port work will span many AI conversations. When my context window approaches full, I update `automaker/python/docs/HANDOFF.md` with the current state and stop, handing off to a fresh context.

- Memory (machine-local) captures **durable** rules and decisions.
- `HANDOFF.md` (committed on `python-port`) captures **transient** state of active work.

They complement — they don't duplicate.
