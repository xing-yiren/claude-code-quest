---
id: 8
title: 使用 Skills
phase: 1
difficulty: 2
type: usage
---

## 目标

学会浏览和调用 Claude Code 的技能（Skills），扩展 Claude 的能力。

## 任务

Skills 是 Claude Code 的扩展能力。有些是内置的（如 `/simplify`、`/claude-api`），有些是文件技能（放在 `.claude/skills/` 目录下）。

1. 输入 `/skills` 浏览当前可用的所有技能
2. 找到本教程对应的技能（应该叫 "tutorial" 或 "quest"）
3. 找一个你感兴趣的其他技能，试试调用它

完成后告诉我：你看到了哪些技能？你尝试了哪个技能？它做了什么？

## 验证

告诉我你浏览了哪些技能，尝试了哪一个，它的作用是什么。

## 提示

- `/skills` 命令会展示所有可用技能
- 技能可以用 `/技能名` 直接调用
- 你也可以输入 `/` 看自动补全列表中带有技能标记的条目
- 文件技能放在 `.claude/skills/<技能名>/SKILL.md`
- 本教程本身就是一个技能！
