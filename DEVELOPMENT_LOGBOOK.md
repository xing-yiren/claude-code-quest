# Development Logbook

This log tracks tutorial development decisions, pushed changes, and remaining work for Claude Code Quest.

## How to use this file

- Add a new entry after each meaningful development push.
- Keep entries concise: what changed, why, and any follow-up.
- When a todo is completed, check it off and mention the commit that completed it.

## Pushed changes

### 2026-05-15 — Project context migration

Commit: pending

- Added project-level `CLAUDE.md` so future Claude Code sessions launched from this repository inherit the working context.
- Documented tutorial structure, level design principles, progressive disclosure rules, Git workflow, and maintenance checklist.
- Pointed future work at `DEVELOPMENT_LOGBOOK.md` as the project todo source.

Why:
- Most development happened from a different working directory, so new sessions launched in this repo needed a durable project context handoff.

### 2026-05-15 — Progressive long-task presentation

Commit: `75d25de Make long tutorial tasks progressive`

- Added a general `## 分步任务` rule in `.claude/skills/tutorial/SKILL.md`.
- Refactored Level 4 Git workflow so the first render shows the goal and first step, then reveals later steps progressively.
- Removed user-facing engine notes from Level 11 MCP advanced content.

Why:
- Long up-front checklists made levels feel like documentation dumps.
- Progressive disclosure keeps the tutorial interactive and closer to a guided lesson.

### 2026-05-15 — Early Git workflow lesson

Commit: `233abbe Insert early Git workflow lesson`

- Added new Level 4: `Git 工作流基础`.
- Renumbered the tutorial from 24 to 25 levels.
- Shifted model, session, CLAUDE.md, skills, plan mode, MCP, subagent, context, architecture, and bonus levels forward by one.
- Updated README and tutorial skill metadata to reflect 25 levels.

Why:
- Official Claude Code quickstart teaches Git early.
- After file operations, users should learn how Claude Code inspects, explains, and saves changes safely.

### 2026-05-15 — Align tutorial with Claude Code workflows

Commit: `4042846 Align tutorial with Claude Code workflows`

- Added a global render boundary: `关卡内容` vs `补充说明`.
- Improved Level 8 skills lesson with skills / slash commands / plugins distinctions.
- Improved Level 9 plan mode lesson with Explore → Plan → Implement → Verify/Commit framing.
- Strengthened Level 11 subagent lesson around protecting main context.
- Strengthened Level 13 context management with `/btw` and subagent context isolation.
- Reworked Level 23 from a toy greeting skill into a reusable `docs-review` workflow skill.

Why:
- Official docs emphasize daily workflows and context management, not just feature names.

### 2026-05-15 — Progressive GitHub MCP tutorial

Commit: `85c02fb Make GitHub MCP tutorial progressive`

- Split Level 10/11 MCP lesson into a short base task and optional progressive GitHub MCP setup.
- Added skill-level rules for progressive optional sections.

Why:
- Full GitHub MCP setup was too long for the first render.
- Users should complete the MCP concept first, then opt into advanced setup.

### 2026-05-15 — Expanded GitHub MCP setup

Commit: `1e96abc Expand GitHub MCP setup guide`

- Added concrete GitHub MCP setup steps using Docker and `claude mcp add`.
- Added read-only mode guidance via `GITHUB_READ_ONLY=1`.
- Clarified that `git` / `gh` remain preferable for local commit, branch, and push workflows.

Why:
- The optional MCP lesson needed a real end-to-end setup path.

### 2026-05-15 — Optional GitHub MCP challenge

Commit: `4c92ab7 Add optional GitHub MCP challenge`

- Added a GitHub MCP optional challenge to the MCP level.
- Kept GitHub MCP configuration out of the required pass condition.

Why:
- GitHub MCP is useful but depends on account, token, and permission setup.

### 2026-05-15 — Tutorial rendering and verification rules

Commits:
- `8973f72 Relax tutorial rendering guidance`
- `4b2faf5 Standardize tutorial flow rules`
- `f3adda0 Clarify CLAUDE.md lesson verification`

- Standardized end-of-level `📌 本关收获` recaps.
- Added the rule that verification questions must wait for user answers.
- Relaxed exact 1:1 rendering into a task consistency rule.
- Clarified Level 7/8 CLAUDE.md verification so file creation alone is not enough.

Why:
- The tutorial should be consistent without becoming rigid.
- Game Master explanations should help, not replace learner answers.

## Todo list

### Curriculum structure

- [x] Add early Git workflow lesson after file operations. Completed in `233abbe`.
- [x] Convert long Git workflow lesson into progressive checkpoints. Completed in `75d25de`.
- [x] Keep MCP base lesson short and make GitHub MCP optional/progressive. Completed in `85c02fb` and `1e96abc`.
- [ ] Add or repurpose a lesson for verification-first workflow: tests, screenshots, expected outputs, and success criteria.
- [ ] Add or repurpose a lesson for permissions / sandbox / auto mode.
- [ ] Add or repurpose a lesson for headless CLI automation with `claude -p`, pipes, and CI-style usage.
- [ ] Decide whether hooks/plugins/multi-surface overview should be a new level, a bonus section, or additions to existing levels.

### Level quality

- [x] Add `关卡内容` vs `补充说明` render boundary. Completed in `4042846`.
- [x] Prevent verification self-answering. Completed in `4b2faf5`.
- [x] Add consistent `📌 本关收获` recaps. Completed in `4b2faf5`.
- [ ] Review all long usage levels for progressive disclosure opportunities.
- [ ] Re-test `/tutorial go 4` end-to-end with the new progressive Git flow.
- [ ] Re-test `/tutorial list` after the 25-level renumbering.
- [ ] Re-test Level 8 CLAUDE.md and Level 7 session-management special verification after renumbering.

### Documentation and maintenance

- [x] Update README for 25 levels. Completed in `233abbe`.
- [x] Keep this development logbook. Started in this entry.
- [ ] Keep README and `.claude/skills/tutorial/SKILL.md` in sync whenever level count or command behavior changes.
- [x] Add a short contributor note explaining how to update this logbook and check off todos. Completed in pending context-migration commit.

## Open questions

- Should the curriculum stay exactly 25 levels, or should missing workflow topics become a separate optional advanced track?
- Should progress migration be automated in `SKILL.md`, or is manual migration enough for this development/testbed phase?
- Should practical levels create disposable practice folders by convention, for example `ccq-*`, to avoid polluting real projects?
