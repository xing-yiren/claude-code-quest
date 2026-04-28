# Claude Code Quest

An interactive, game-like tutorial for learning Claude Code — from basic usage to source architecture mastery.

## How It Works

This is a **Claude Code file skill**. No plugins, no source-code modifications, no extra installs. Just drop the `.claude/` folder into your project and type `/tutorial` in Claude Code.

```
User: /tutorial
Claude: ┌──────────────────────────────────────┐
        │  Claude Code Quest                   │
        │  进度: Level 6/24  (5 已完成)         │
        │                                      │
        │  📖 会话恢复与回退                    │
        │  阶段 1 · 难度 ★★ · 实操             │
        │                                      │
        │  学会恢复之前的会话，并在需要时回退   │
        │  到较早的对话节点重新尝试...          │
        └──────────────────────────────────────┘
```

## 24 Levels, 3 Phases + 1 Bonus

| Phase | Levels | Focus |
|-------|--------|-------|
| 1 — Usage | 1–12 | Learn Claude Code through guided hands-on tasks |
| 2 — Source | 13–17 | Understand Claude Code architecture from the source |
| 3 — Deep Dive | 18–23 | Explore advanced systems and build your own skill |
| Bonus | 24 | Learn an adjacent third-party workflow tool |

## Learning Philosophy

Claude Code Quest is designed to progress in three steps:

1. **Learn the basics** — slash commands, files, models, memory, planning
2. **Practice real workflows** — session recovery, custom model config, subagents, agent teams
3. **Understand the internals** — context, tools, security, memory, tasks, UI, and skills

As the tutorial goes on, levels become more **project-based**. Instead of abstract Q&A, later levels are designed around small practical outcomes so you learn each feature by using it in a realistic workflow.

## Highlights

- **Guided usage lessons** for Claude Code fundamentals
- **Hands-on workflow levels** like session recovery, subagent task delegation, and agent teams
- **Source-reading phases** for understanding how Claude Code works internally
- **Build-your-own-skill finale** as a concrete final project
- **Zero-invasion design** — implemented entirely as a file skill

## Quick Start

```bash
# In your project directory
git clone https://github.com/xing-yiren/claude-code-quest.git .quest-tmp
cp -r .quest-tmp/.claude .
rm -rf .quest-tmp

# Start Claude Code and type:
#   /tutorial
```

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed
- A Claude Code-compatible project directory

## Repository Structure

```text
.claude/
├── skills/
│   └── tutorial/
│       └── SKILL.md              # Tutorial game engine
└── tutorial/
    ├── progress.json             # Player progress (created at runtime)
    └── levels/
        ├── 01-welcome.md
        ├── ...
        └── 24-cc-switch.md
```

## License

MIT
