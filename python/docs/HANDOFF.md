# Port Handoff

**Last updated:** 2026-04-23 (L0 requirements drafted)
**Current branch:** `python-port`

## Current status

- Ground rules and repo architecture established. See `../../PORT_RULES.md` for substantive port rules and the Ground Rules section for process rules.
- Repo configured with three remotes: `origin` (GitHub fork `mgeppert/automaker`), `upstream` (read-only `AutoMaker-Org/automaker`, push URL deliberately broken), `gitea` (local NAS).
- `python-port` branch is where all port work lives; `main` mirrors upstream.
- Graphify analysis complete at `../../graphify-out/` (local only, excluded from git via `.git/info/exclude`). See `GRAPH_REPORT.md` there for god nodes and community structure.
- **L0 requirements drafted (Pass 1 complete).** 27 fuzzy Feature-level requirements written at `../requirements/REQ-*.md`. All in `status: draft`, all have `Test plan: (to be decomposed)`.
- No Python implementation yet; only scaffolding and requirement docs.

## L0 Features (REQ-1000 through REQ-27000)

| ID | Title |
|---|---|
| REQ-1000 | Worktree Management |
| REQ-2000 | Git Operations |
| REQ-3000 | Agent Execution Framework |
| REQ-4000 | Provider System |
| REQ-5000 | Claude Provider |
| REQ-6000 | Codex Provider |
| REQ-7000 | Cursor Provider |
| REQ-8000 | Copilot Provider |
| REQ-9000 | Gemini Provider |
| REQ-10000 | OpenCode Provider |
| REQ-11000 | Mock Provider |
| REQ-12000 | Feature Management |
| REQ-13000 | Pipeline Orchestration |
| REQ-14000 | Spec Parsing and Ideation |
| REQ-15000 | Context File Loading |
| REQ-16000 | Project Setup Flow |
| REQ-17000 | Authentication and Credentials |
| REQ-18000 | Settings Persistence |
| REQ-19000 | HTTP and WebSocket API Surface |
| REQ-20000 | Terminal PTY Integration |
| REQ-21000 | Dev Server Integration |
| REQ-22000 | GitHub Integration |
| REQ-23000 | MCP Integration |
| REQ-24000 | Startup Doctor (net-new) |
| REQ-25000 | Logging Infrastructure |
| REQ-26000 | Cross-Platform CI (net-new) |
| REQ-27000 | UI Adaptation For Web Only |

## Next step

**Review L0 drafts with Mike before beginning L1 decomposition.** Expect:

- Some L0s to be renamed, split, or merged based on review.
- Mike to flag missing Features or questionable inclusions.
- Agreement on which L0 to decompose first (likely REQ-1000 Worktree Management or REQ-17000 Authentication since both are load-bearing).

After review: begin Pass 2 (L1 decomposition) on the agreed starting Feature. Each L1 child gets a `REQ-<parent>.<N>000-<slug>.md` file using TEMPLATE.md; parent's `Children:` list is updated; parent's status moves to `decomposing`.

## In-flight work

None — awaiting review of L0 drafts.

## Open questions

- **Review order for L1 decomposition:** which L0 to decompose first? Suggestion: REQ-1000 (Worktree — the load-bearing spine) or REQ-24000 (Startup Doctor — simple, self-contained, good way to shake out the L1→L2→tests workflow).
- **Scaffolding before or after L1?** Whether to stand up the FastAPI + pytest + doctor skeleton before writing L1s, or after. Default: after. L1 decomposition doesn't require running code.
- **`source:` field quality at L0 is folder-level.** During L1 decomposition, each leaf gets a precise `apps/server/src/.../file.ts::function()` pointer.
- **TypeScript UI dependencies (REQ-15000 on `@automaker/utils`, REQ-12000 on `@automaker/types`, etc.):** some shared libs are used by both server AND UI. Port decisions here (keep TS, port to Python + emit TS types, etc.) are deferred to the L1/L2 decomposition of the affected Feature.

## Pointers

- **Port Rules (canonical):** `../../PORT_RULES.md`
- **Requirements directory:** `../requirements/`
  - Template: `../requirements/TEMPLATE.md`
  - Conventions: `../requirements/README.md`
  - L0 files: `../requirements/REQ-*.md`
- **Graphify report (local only):** `../../graphify-out/GRAPH_REPORT.md`
- **Outer workspace orientation:** `../../../CLAUDE.md`
- **AI memory (local only):** `~/.claude/projects/-home-mgeppert-git-work-AngeticCoding/memory/`

## Recent course corrections

- Filename convention locked as `REQ-<ID>-<Brief_Title>.md` (underscores in title, Title Case) — 2026-04-23.
