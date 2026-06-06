# Agent continuity — quick reference

## Mandatory

**`.agent/SESSION.md` is the single source of truth.** Every agent (including all personas) MUST:

1. Read SESSION at session start (`/resume`)
2. Work from SESSION Goal / Next / Decisions
3. Update SESSION at session end (`/handoff`)

Never substitute CodeGraph, grep, or chat history for SESSION when resuming work.

## Files

| Path | Role |
|------|------|
| `.agent/SESSION.md` | Live handoff (commit to git) |
| `.agent/SESSION.template.md` | Schema reference |
| `.agent/README.md` | Human overview |
| `tasks/todo.md` | Task checklist (workflow) |
| `SPEC.md` | Feature spec (workflow) |

## Commands

| Command | When |
|---------|------|
| **`/resume`** | Start of session — read SESSION, summarize, continue |
| **`/handoff`** | End of session — write SESSION, sync tasks |

## Read order (resume)

1. `.agent/SESSION.md`
2. `tasks/todo.md`
3. Linked spec from SESSION Pointers

## Install

```bash
npx class-ai-agent
```

Creates `.agent/` and seeds `SESSION.md` from template.

## Rules

- **Cursor:** `.cursor/rules/agent-continuity.mdc` (`alwaysApply`)
- **Claude:** `.claude/rules/agent-continuity.md`
- **Kiro:** `.kiro/steering/agent-continuity.md` (`inclusion: always`)
- **Personas:** `.cursor/agents/*.md`, `.claude/agents/*.md`, `.kiro/agents/*.md` (each includes mandatory SESSION section)

## Skill

`.cursor/skills/agent-continuity/SKILL.md` — full handoff/resume checklists.
