# Agent session

> Cross-tool handoff state for Cursor, Claude Code, and Kiro. Update at session end (`/handoff`) or phase changes; read at session start (`/resume`).

## Meta

| Field | Value |
|-------|-------|
| **Updated** | 2026-06-06 |
| **Phase** | build |
| **Tool** | cursor |
| **Persona** | _(maintainer)_ |

## Goal

Enforce **`.agent/SESSION.md`** as the mandatory single source of truth for all AI agents (Cursor, Claude Code, Kiro) — every persona reads it at session start and updates it at session end; no agent replans from scratch or substitutes CodeGraph/grep for handoff state.

## Done

- Diagnosed `Error: task must be a non-empty string` — wrong args on `codegraph_context` (`query`/`limit` vs `task`/`maxNodes`).
- Documented parameter split in `.cursor/rules/codegraph.mdc`, `.cursor/references/codegraph.md`, `.claude/`, `.kiro/` (via `npm run sync:kiro`).
- Clarified in agent-continuity rules: resume handoff = Read `SESSION.md`, not CodeGraph.
- Added **Mandatory (all agents)** section to agent-continuity rules (`.cursor/`, `.claude/`, `.kiro/`).
- Added **Session continuity (mandatory)** block to all 30 agent personas (`.cursor/agents/`, `.claude/agents/`, `.kiro/agents/`).
- Updated `AGENTS.md`, `CURSOR.md`, `CLAUDE.md`, `.agent/README.md`, and agent-continuity references/skill.

## In progress

- _(none)_
- **Blockers:** none

## Next

1. Review and commit agent scaffolding + SESSION enforcement when approved (large untracked trees on `develop`).
2. Create `tasks/todo.md` when feature work begins (link from Pointers).
3. Run `/handoff` after each meaningful session end.

## Decisions

- **`.agent/SESSION.md` is mandatory** for every agent persona and every session — not optional, not superseded by chat history or CodeGraph.
- Session resume uses **`.agent/SESSION.md` + `/resume`**, not `codegraph_context`.
- `codegraph_context` requires **`task`**; `codegraph_search` requires **`query`**.
- Commit `SESSION.md` to git so the whole team and any IDE can resume.

## Gotchas

- Calling `codegraph_context` with `{ "query": "...", "limit": 15 }` → `task must be a non-empty string`.
- CodeGraph MCP may need `projectPath` if workspace root is not detected.
- Repo is **Kestra** (Java orchestration) on branch **`develop`** — agent scaffolding is additive, not the upstream product.
- Large untracked agent config trees — review before commit.

## Pointers

| Item | Location |
|------|----------|
| Spec | _(none — agent scaffolding maintenance)_ |
| Tasks | _(no `tasks/todo.md` yet)_ |
| Branch | `develop` |
| Key files | `.agent/SESSION.md`, `.agent/README.md`, `.cursor/rules/agent-continuity.mdc`, `.cursor/commands/resume.md`, `.cursor/commands/handoff.md`, `.cursor/agents/*.md`, `AGENTS.md` |
