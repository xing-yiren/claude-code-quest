---
id: 20
title: 记忆系统
phase: 3
difficulty: 3
type: source
---

## 目标

理解 Claude Code 的持久记忆系统——如何跨会话记住用户信息和偏好。

## 背景

Claude Code 能在不同会话之间记住用户信息。这个记忆系统基于文件系统，存储在 `.claude/memory/` 目录中。

## 代码节选

```
文件系统结构：
.claude/
└── memory/
    ├── MEMORY.md              ← 索引文件，列出所有记忆
    ├── user_role.md           ← 用户角色信息
    ├── feedback_testing.md    ← 反馈偏好
    └── project_goals.md       ← 项目目标

MEMORY.md 格式（索引）：
  - [User Role](user_role.md) — 资深开发者，偏好 Rust
  - [Testing Feedback](feedback_testing.md) — 不要 mock 数据库

4 种记忆类型：
  1. user     → 用户角色、目标、知识水平
  2. feedback → 用户对 AI 行为的偏好和纠正
  3. project  → 项目目标、约束、当前状态
  4. reference→ 外部系统信息位置

AutoDream 机制（自动记忆整理）：
  - 冷却期: 24 小时（避免频繁触发）
  - 积累: 5 次会话积累（收集足够信息）
  - 文件锁: 防止并发写入冲突
  - 条件满足后自动触发记忆整理
```

**写入流程**：
1. 对话中检测到值得记忆的信息
2. 写入独立文件（含 frontmatter：name, description, type）
3. 在 MEMORY.md 中添加索引条目
4. 下次对话时自动加载

## 问题

1. 4 种记忆类型分别存储什么内容？给每种类型举一个例子。
2. MEMORY.md 和独立记忆文件是什么关系？
3. AutoDream 的触发条件是什么？为什么需要冷却期？

## 期望答案

1. user=用户角色信息、feedback=偏好纠正、project=项目状态、reference=外部信息位置
2. MEMORY.md 是索引（目录），独立文件存具体内容
3. 24 小时冷却 + 5 次会话积累；冷却期避免频繁触发消耗 token，积累期收集足够信息才有意义
