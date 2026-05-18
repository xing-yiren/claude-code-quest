# CLAUDE.md

This file gives Claude Code project-specific context for working on **claude-code-quest**.

## Project overview

Claude Code Quest is an interactive, game-like tutorial for learning Claude Code. It is implemented as a **Claude Code file skill** rather than application code.

- Public repo: `https://github.com/xing-yiren/claude-code-quest`
- Skill entry point: `.claude/skills/tutorial/SKILL.md`
- Level files: `.claude/tutorial/levels/NN-slug.md`
- Progress file used during local testing: `.claude/tutorial/progress.json`
- Development history and todo list: `DEVELOPMENT_LOGBOOK.md`

## Current curriculum shape

The tutorial currently has **25 levels** across 3 phases + 1 bonus:

| Phase | Levels | Focus |
|-------|--------|-------|
| Phase 1 — Basics | 1–14 | Usage: slash commands, file ops, Git workflow, model switching, custom model, session recovery, CLAUDE.md, skills, plan mode, MCP, subagents, agent teams, context management |
| Phase 2 — Architecture | 15–19 | Source: QueryEngine, tool system, coordinator-worker, context compression, skills system |
| Phase 3 — Deep Dive | 20–24 | Source + usage: security model, memory system, task system, terminal UI, build-your-skill |
| Bonus | 25 | cc-switch multi-config management |

## Important files

- `.claude/skills/tutorial/SKILL.md`
  - The Game Master rules and command dispatcher.
  - Update this when changing tutorial flow, verification rules, progressive disclosure behavior, or command semantics.

- `.claude/tutorial/levels/*.md`
  - One level per file.
  - Filenames and frontmatter `id` must match.
  - Keep user-facing level content separate from Game Master engine instructions.

- `DEVELOPMENT_LOGBOOK.md`
  - Record meaningful development pushes and decisions.
  - Keep the todo list current.
  - Check off completed items with the commit that completed them.

- `README.md`
  - Public-facing project summary and install/use instructions.
  - Keep level count and phase ranges in sync with `SKILL.md` and level files.

## Tutorial design principles

### Separate level content from Game Master notes

When rendering a level, keep a visible boundary between:

1. **关卡内容**
   - Comes from the level file.
   - Defines what the learner must do to pass.
   - Includes goal, task, verification question, and hints.

2. **补充说明**
   - Adaptive context or recommendations inferred by Claude.
   - Must be labeled as supplementary.
   - Must not create new pass conditions.

Do not mix extra recommendations into the required task body.

### Do not put engine-only notes in level files

Level files are user-facing. Avoid text such as:

- "Game Master 注意"
- "do not show this on first render"
- internal implementation notes about checkpoint rendering

Put those rules in `.claude/skills/tutorial/SKILL.md` instead.

### Use progressive disclosure for long tasks

For long usage tasks, prefer:

- Short first render: goal + overall task + first actionable step
- Later checkpoints revealed only after the user completes or asks about the current step

Supported patterns:

- `## 分步任务` for required multi-step lessons
- `## 进阶入口` + `## 进阶教程` for optional advanced tracks

Do not dump long command lists or setup instructions all at once.

### Ask verification questions and wait

If a level asks a verification question, ask it and stop. Do not answer it yourself in the same turn.

After the user answers:

- Grade leniently.
- Pass if the core concepts are present.
- If incomplete, explain the missing piece and offer a hint.

### End passed levels with a recap

Every passed level should end with:

```text
📌 本关收获
- 核心知识点 1
- 核心知识点 2
- 核心知识点 3
```

Use 2–3 short bullets. This recap comes **after** the user answers the verification question.

### Prefer practical, project-based learning

Later levels should feel like guided mini-projects rather than abstract Q&A whenever possible.

Good examples:

- Git workflow in a disposable `ccq-git-practice/` repo
- GitHub MCP as an optional progressive setup
- `docs-review` skill as a reusable workflow

## Git and GitHub workflow

This repository is a real Git repo. Normal development workflow:

1. Make changes locally.
2. Review `git status` and `git diff`.
3. Commit with a clear message.
4. Push to `origin master` when the user asks to sync.

Important:

- Do not push unless the user asks or has clearly approved the sync.
- For tutorial practice levels, do not run `git init` in the project root. Use disposable `ccq-*` practice folders instead.
- Local commit/push behavior should be taught as more sensitive than read-only inspection.

## Current known work / todo

Always check `DEVELOPMENT_LOGBOOK.md` before starting significant work. It is the authoritative project todo list.

Current likely next topics:

- Verification-first workflow level
- Permissions / sandbox / auto mode level
- Headless CLI automation with `claude -p`
- Hooks/plugins/multi-surface overview
- Retesting Level 4 progressive Git flow
- Retesting `/tutorial list` after 25-level renumbering

## When updating levels

Before committing:

1. Ensure filename prefix and frontmatter `id` match.
2. Ensure the level has `## 目标`, `## 任务`, `## 验证`, and `## 提示` unless there is a clear reason.
3. Ensure user-visible content does not contain engine-only instructions.
4. If adding long tasks, use `## 分步任务` or optional advanced sections.
5. Update `README.md`, `SKILL.md`, and `DEVELOPMENT_LOGBOOK.md` when level count, command behavior, or major curriculum structure changes.

## Testing useful commands

Common manual checks:

```text
/tutorial list
/tutorial go 4
/tutorial go 8
/tutorial go 11
```

For Git state:

```bash
git status
git diff
git log --oneline -5
```
