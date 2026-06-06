# AI agent instructions

Project guidance for AI coding agents:

| Tool | Hub |
|------|-----|
| **Cursor** | [`.cursor/CURSOR.md`](.cursor/CURSOR.md) |
| **Kiro** | [`.kiro/KIRO.md`](.kiro/KIRO.md) |
| **Claude Code** | [`.claude/CLAUDE.md`](.claude/CLAUDE.md) |

- **Cursor:** `.cursor/rules/` (`.mdc`), `.cursor/commands/`, `.cursor/mcp.json`
- **Kiro:** `.kiro/steering/` (`*.md`), `.kiro/commands/`, `.kiro/settings/mcp.json`
- **Claude Code:** `.claude/rules/`, `.claude/commands/`

**Cross-tool continuity (mandatory):** committed [`.agent/SESSION.md`](.agent/SESSION.md) is the **single source of truth** for in-flight work. **Every agent** — including all personas — must read it at session start (`/resume`), work from its Goal/Next/Decisions, and update it at session end (`/handoff`). See [`.agent/README.md`](.agent/README.md) and hub docs.

Keep **`.claude/`**, **`.cursor/`**, and **`.kiro/`** in sync when you change workflows or standards. After editing `.cursor/`, run `npm run sync:kiro` in the **class-ai-agent** repo to refresh `.kiro/`. To refresh vendored Supabase skills from upstream, run `npm run sync:supabase-skills`.
