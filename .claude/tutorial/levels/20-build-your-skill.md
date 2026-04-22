---
id: 20
title: 创建自己的 Skill
phase: 3
difficulty: 3
type: usage
---

## 目标

动手创建一个属于自己的 Claude Code 技能（Skill），巩固对技能系统的理解。

## 任务

现在你已经了解了技能系统的工作原理（第 15 关），是时候亲手创建一个了！

1. 在 `.claude/skills/` 目录下创建一个名为 `hello-quest` 的文件夹
2. 在里面创建 `SKILL.md` 文件，内容如下：
   ```markdown
   ---
   description: "一个友好的问候技能"
   ---

   你是一个友好的助手。用户说什么，你就用中文回复 "你好！" + 用户说的话。
   如果用户说 "完成"，就回复 "太棒了！" 然后结束。
   ```
3. 输入 `/hello-quest` 测试你的技能
4. 和你的技能聊几句，确保它正常工作
5. 完成后告诉我

**额外挑战（可选）**：
给你的技能添加 `allowedTools` 配置，允许它使用 Read 和 Glob 工具。修改 SKILL.md 的 frontmatter：

```markdown
---
description: "一个友好的问候技能，也能查看文件"
allowedTools: [Read, Glob]
---
```

## 验证

我会检查 `.claude/skills/hello-quest/SKILL.md` 是否存在且内容正确。

## 提示

- 文件技能放在 `.claude/skills/<技能名>/SKILL.md`
- 修改 SKILL.md 后 Claude Code 会自动热重载（几秒内）
- YAML frontmatter 中 `description` 是必填项
- 技能 prompt 会注入到模型上下文中，写清楚角色和行为
- 完成这个关卡后，你就是一个正式的 Claude Code 技能开发者了！
