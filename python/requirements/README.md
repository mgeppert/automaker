# Requirements — Automaker Python port

This directory contains the requirements for the Python port of Automaker. The rules governing how requirements are written live in `../../PORT_RULES.md` (Ground Rules section).

## Directory layout

```
requirements/
├── README.md          (this file)
├── TEMPLATE.md        (copy when creating a new requirement)
├── REQ-1000-<slug>.md (one file per requirement)
├── REQ-2000-<slug>.md
├── ...
└── TESTS.md           (planned — rollup of all Test plans, generated later)
```

## ID scheme (summary)

Dotted hierarchical with 1000-step spacing:

- L0 Features: `REQ-1000`, `REQ-2000`, `REQ-3000`, ...
- L1: `REQ-1000.1000`, `REQ-1000.2000`, ...
- L2: `REQ-1000.1000.1000`, ...

The `REQ-` prefix makes IDs grep-able. The 1000-step spacing leaves room to insert siblings later without renumbering the rest.

See the Ground Rules section of `../../PORT_RULES.md` for the full convention (including traceability, test plans, and pytest markers).

## Lifecycle

Every requirement moves through these `status` values:

| Status | Meaning |
|---|---|
| `draft` | Written but not reviewed. |
| `decomposing` | Parent; children being created this pass. |
| `ready` | Leaf; singular, has a Test plan, ready to implement. |
| `implementing` | Code being written. |
| `done` | All tests pass. |

A parent is `done` when all its children are `done`.

## Creating a new requirement

1. Copy `TEMPLATE.md` to `REQ-<ID>-<slug>.md` (e.g. `REQ-1000-worktree-management.md`).
2. Fill the frontmatter (`id`, `title`, `parent`, `level`, `status`, `source`, `depends_on`).
3. Write the `Statement` and `User-visible behavior` sections.
4. For L0 / intermediate parents: leave `Test plan` empty; children will carry the tests. Populate `Children` with the REQ IDs once decomposed.
5. For leaves: write the `Test plan` (one pytest function per singular assertion) and set `Children` to `none`.
6. Update the parent's `Children` list to include this new file.

## Filenames

Filenames include a human-readable slug after the ID for quick navigation: `REQ-1000.1000-execute-agent-run.md`. The slug is advisory — the ID is canonical.

## Tests

Every leaf requirement's Test plan names one or more pytest functions. The pytest tests themselves live under `../tests/` (structure mirrors the requirement tree loosely). Each test function:

- Is named `test_REQ_<id_with_underscores>_<descriptive_suffix>`.
- Carries exactly one `@pytest.mark.req("REQ-...")` marker.
- Asserts exactly what the Test plan entry describes.
