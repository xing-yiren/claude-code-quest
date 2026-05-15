---
id: 23
title: 创建自己的 Skill
phase: 3
difficulty: 3
type: usage
---

## 目标

动手创建一个属于自己的 Claude Code 技能（Skill），巩固对技能系统的理解。

## 任务

现在你已经了解了技能系统的工作原理（第 18 关），是时候亲手创建一个更接近真实工作流的 Skill 了！

1. 在 `.claude/skills/` 目录下创建一个名为 `docs-review` 的文件夹
2. 在里面创建 `SKILL.md` 文件，内容如下：
   ```markdown
   ---
   description: "Review Markdown docs for clarity, structure, and missing next steps"
   allowed-tools: [Read, Glob, Grep]
   ---

   你是一个文档审查助手。请审查用户指定的 Markdown 文件或目录。

   重点检查：
   1. 标题结构是否清晰
   2. 是否有 TODO、占位内容或过期说明
   3. 是否缺少安装、使用、验证或下一步说明
   4. 是否有可以简化的长段落

   输出格式：
   - 先给 3 条以内总体结论
   - 再列出具体文件和建议
   - 不要直接修改文件，除非用户明确要求
   ```
3. 输入 `/docs-review` 测试你的技能
4. 让它审查一个 Markdown 文件或目录，例如：
   - `请审查 README.md`
   - `请审查 .claude/tutorial/levels/`
5. 完成后告诉我这个 Skill 做了什么、为什么它比一次性 prompt 更适合复用

**额外挑战（可选）**：
把这个 skill 改成只在用户明确要求时才编辑文件，并在 prompt 里写清楚“先审查，后询问是否修改”。

## 验证

我会检查：

1. `.claude/skills/docs-review/SKILL.md` 是否存在
2. frontmatter 和 prompt 是否包含文档审查目标
3. 你是否能说明这个 Skill 的复用价值，以及它和一次性 prompt 的区别

## 提示

- 文件技能放在 `.claude/skills/<技能名>/SKILL.md`
- 修改 SKILL.md 后 Claude Code 会自动热重载（几秒内）
- YAML frontmatter 中 `description` 是必填项
- 真实有价值的 skill 往往围绕“重复出现的工作流”设计，而不是一次性的玩具对话
- 如果一个 prompt 你会反复使用 5 次以上，它就值得做成 skill
- 完成这个关卡后，你就能开始为自己或团队封装可复用工作流了！
