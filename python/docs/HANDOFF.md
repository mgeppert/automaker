# Port Handoff

**Last updated:** 2026-04-23
**Current branch:** `python-port`

## Current status

- Ground rules and repo architecture established. See `../../PORT_RULES.md` for substantive port rules and the Ground Rules section for process rules.
- Repo configured with three remotes: `origin` (GitHub fork `mgeppert/automaker`), `upstream` (read-only `AutoMaker-Org/automaker`, push URL deliberately broken), `gitea` (local NAS).
- `python-port` branch is where all port work lives; `main` mirrors upstream and is touched only by merges from `upstream/main`.
- Python skeleton at `../` (this file's parent's parent). Nothing implemented yet.
- Graphify analysis complete at `../../graphify-out/` (local only, excluded from git via `.git/info/exclude`). See `GRAPH_REPORT.md` there for god nodes and community structure.
- Requirements directory at `../requirements/` with template and README. No requirements written yet.

## Next step

**Draft the L0 (not-good, Feature-level) requirements list.** Target ~15–25 Features based on Graphify's god nodes and community structure. Each L0 becomes a requirement file at `../requirements/REQ-<N>000-<slug>.md` using `TEMPLATE.md`. Expect these to be fuzzy — they will be decomposed in later passes.

Likely starting Features (from Graphify):

- Worktree management (god node #1 — `createWorktreeRoutes()` at 64 edges)
- Agent execution via Claude provider (IdeationService + AgentExecutor + worktree spine)
- Feature management (Kanban state, feature CRUD)
- Multi-provider support (Codex, Cursor, Copilot, Gemini, OpenCode) — each a candidate Feature
- Git operations subsystem (`execGitCommand` at god node #5)
- HTTP + WebSocket API surface (wire contract the UI expects)
- Settings / credentials persistence
- Project setup flow (`createSetupRoutes()` at god node #4)
- Startup doctor / dependency check (net-new, not in JS)
- Mock provider mode (parity with `AUTOMAKER_MOCK_AGENT=true`)

## In-flight work

None. Ground rules phase just completed; requirements drafting not yet started.

## Open questions

- **Filename slugs:** `REQ-1000-worktree-management.md` or `REQ-1000.md`? Default: slug for readability.
- **Scaffolding order:** write L0 requirements first, then stand up the FastAPI/pytest scaffolding? Or scaffold first so we have something to run tests against? Default: requirements first (PORT_RULES follows that plan).
- **Electron audit scope:** `getElectronAPI()` is a top-10 god node — how exhaustive should the UI audit of `window.electron?` call sites be? Probably its own Feature or L1 requirement under the UI adaptation Feature.

## Pointers

- **Port Rules (canonical):** `../../PORT_RULES.md`
- **Requirements template:** `../requirements/TEMPLATE.md`
- **Requirements index and conventions:** `../requirements/README.md`
- **Graphify report (local only):** `../../graphify-out/GRAPH_REPORT.md`
- **Outer workspace orientation:** `../../../CLAUDE.md`
- **AI memory (local only):** `~/.claude/projects/-home-mgeppert-git-work-AngeticCoding/memory/`

## Recent course corrections

None yet — ground rules phase was additive.
