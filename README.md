# Claude Code Quest

An interactive, game-like tutorial for learning Claude Code — from basic usage to source architecture mastery.

## How It Works

This is a **Claude Code file skill**. No plugins, no modifications, no extra installs. Just drop the `.claude/` folder into your project and type `/tutorial` in Claude Code.

```
User: /tutorial
Claude: ┌──────────────────────────────────────┐
        │  Claude Code Quest                   │
        │  进度: ████░░░░░░ 3/20              │
        │                                      │
        │  📖 关卡 3: 文件操作                 │
        │  难度: ★☆☆                           │
        │                                      │
        │  让 Claude Code 在你的项目中创建      │
        │  一个文件并修改它...                  │
        └──────────────────────────────────────┘
```

## 20 Levels, 3 Phases

| Phase | Levels | Topic |
|-------|--------|-------|
| 1 — Basics | 1–10 | Learn to use Claude Code |
| 2 — Architecture | 11–15 | Understand the design |
| 3 — Deep Dive | 16–20 | Master the internals |

## Quick Start

```bash
# In your project directory
git clone https://github.com/YOUR_USERNAME/claude-code-quest.git .quest-tmp
cp -r .quest-tmp/.claude .
rm -rf .quest-tmp

# Start Claude Code and type:
#   /tutorial
```

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed
- A Claude Code-compatible project directory

## License

MIT
