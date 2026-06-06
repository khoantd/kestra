# Agent continuity

Cross-tool handoff lives in **`.agent/SESSION.md`** (committed). Cursor, Claude Code, and Kiro agents share this file.

## Mandatory (all agents)

**Every agent session MUST follow these rules — no exceptions:**

1. **Read `.agent/SESSION.md` first** — before planning, coding, reviewing, or answering architecture questions about in-flight work.
2. **Do not replan from scratch** — if SESSION is current, continue from **Goal**, **In progress**, and **Next**; do not re-discover context via grep, CodeGraph, or chat history alone.
3. **Update SESSION during work** — after meaningful progress, refresh **Done**, **In progress**, and **Next**.
4. **Hand off before exit** — run **`/handoff`** (update `.agent/SESSION.md`) before closing chat, switching tools, or switching personas.
5. **Personas inherit this rule** — invoking specialized agents does not exempt the session from SESSION.

**Never** use `codegraph_context`, grep, or prior chat as a substitute for SESSION when resuming work.

## Session start

1. If **`.agent/SESSION.md`** exists, read it **before** planning or editing code.
2. When the user says **continue**, **resume**, or **pick up**, use **`.claude/commands/resume.md`**.
3. Then read **`tasks/todo.md`** and linked **SPEC** paths from SESSION **Pointers**.

**Do not** call `codegraph_context` with `query` / `limit` for session resume — that tool requires **`task`** and is for code symbols, not handoff state. For continuity, read `.agent/SESSION.md` (and `tasks/todo.md`); use `codegraph_context` only when you need structural code context for the work described in SESSION.

## Session end and phase changes

1. Update **`.agent/SESSION.md`** before ending a session or switching tools — use **`.claude/commands/handoff.md`** when possible.
2. Keep **Done**, **In progress**, and **Next** accurate; do not leave stale **In progress** items.
3. Sync **`tasks/todo.md`** checkboxes when tasks change.

## Security (SESSION.md)

**Never** store in `.agent/SESSION.md`:

- API keys, passwords, tokens, credentials
- PII or customer data

Use issue links, commit SHAs, and file paths instead.

## Workflow integration

| Phase | SESSION `phase` value |
|-------|------------------------|
| Spec | `spec` |
| Plan | `plan` |
| Build | `build` |
| Test | `test` |
| Review | `review` |
| Debug | `debug` |

Set **Meta → Tool** to `cursor`, `claude`, or `kiro` as appropriate.
