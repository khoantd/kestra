# Agent continuity (`.agent/`)

Committed handoff state so **Cursor**, **Claude Code**, and **Kiro** agents can continue the same work without re-discovering context.

## Mandatory for all agents

**`.agent/SESSION.md` is the single source of truth.** Every agent — including specialized personas (`backend`, `code-reviewer`, etc.) — must:

1. **Read `SESSION.md` at session start** (`/resume`)
2. **Work from SESSION Goal / Next / Decisions** — do not replan from scratch
3. **Update `SESSION.md` at session end** (`/handoff`)

Rules are enforced in `.cursor/rules/agent-continuity.mdc` (`alwaysApply: true`) and mirrored in each agent persona file.

## Files

| File | Purpose |
|------|---------|
| **`SESSION.md`** | Live handoff — read at session start, update at session end |
| **`SESSION.template.md`** | Schema reference (do not edit for handoff; copy to `SESSION.md` on fresh install) |
| **`history/`** | _(optional)_ milestone snapshots, e.g. `2025-06-02-feature-x.md` |

## Workflow

1. **Start** — Run `/resume` (or read `SESSION.md` first). Then `tasks/todo.md`, then linked `SPEC.md`.
2. **Work** — Follow `.cursor/`, `.claude/`, or `.kiro/` workflow (`/build`, etc.).
3. **End** — Run `/handoff` to refresh `SESSION.md` before closing the chat or switching tools.

## What to put in `SESSION.md`

- Goal, done / in progress / next steps
- Decisions and gotchas the next agent must know
- Pointers to spec, tasks, branch, key files

## What NOT to put here

- API keys, passwords, tokens, or credentials
- PII or customer data
- Long logs (link to issues or commits instead)

## Commit to git

`SESSION.md` is meant to be **committed** so the whole team and any IDE can resume. Keep it concise and current.
