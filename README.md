# Claude Code Quest

An interactive, game-like tutorial for learning Claude Code — from basic usage to source architecture mastery.

## How It Works

This is a **Claude Code file skill**. No plugins, no modifications, no extra installs. Just drop the `.claude/` folder into your project and type `/tutorial` in Claude Code.

```text
User: /tutorial list
Claude:
Progress: 5/24 completed · Current: Level 5

Phase 1 — Basics
[DONE]    01 欢迎与基本交互
[DONE]    02 斜杠命令入门
[CURRENT] 05 自定义模型配置
[TODO]    06 会话恢复与回退
```

## 24 Levels, 3 Phases + 1 Bonus

| Phase | Levels | Topic |
|-------|--------|-------|
| 1 — Basics | 1–13 | Learn Claude Code usage: slash commands, file ops, model switching, custom model, session recovery, CLAUDE.md, skills, plan mode, MCP, subagents, agent teams, context management |
| 2 — Architecture | 14–18 | Understand the design: QueryEngine, tool system, coordinator-worker, context compression, skills system |
| 3 — Deep Dive | 19–23 | Master the internals: security model, memory system, task system, terminal UI, build-your-skill |
| Bonus | 24 | cc-switch multi-config management |

## Tutorial Commands

The tutorial skill behaves like a small CLI with these supported forms:

- `/tutorial`
- `/tutorial exit`
- `/tutorial hint`
- `/tutorial go <level>`
- `/tutorial skip`
- `/tutorial reset`
- `/tutorial list`

Examples:

```text
/tutorial
/tutorial exit
/tutorial go 14
/tutorial hint
/tutorial list
```

`/tutorial` enters tutorial mode or continues the saved level. `/tutorial exit` pauses tutorial mode and saves progress so you can return later with `/tutorial`.

`/tutorial go <level>` accepts exactly one numeric target level. Forms like `/tutorial go`, `/tutorial go level 5`, or `/tutorial list now` are invalid and should be rejected with a brief usage hint.

## Quick Start

```bash
# In your project directory
git clone https://github.com/YOUR_USERNAME/claude-code-quest.git .quest-tmp
cp -r .quest-tmp/.claude .
rm -rf .quest-tmp

# Start Claude Code and try:
#   /tutorial
#   /tutorial list
#   /tutorial go 5
```

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed
- A Claude Code-compatible project directory

## License

MIT
