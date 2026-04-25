---
id: 17
title: 技能系统
phase: 2
difficulty: 2
type: source
---

## 目标

理解 Claude Code 的技能（Skill）系统——技能如何定义、注册和调用。

## 背景

技能是 Claude Code 的扩展机制。有两种类型：捆绑技能（编译时内置）和文件技能（运行时从文件系统加载）。本教程本身就是一个文件技能。

## 代码节选

```typescript
// 技能定义类型 (src/skills/bundledSkills.ts)
type BundledSkillDefinition = {
  name: string                    // 技能名称
  description: string             // 描述
  getPromptForCommand(args, context) // 返回 prompt 内容
  allowedTools?: string[]         // 允许使用的工具
  userInvocable?: boolean         // 用户是否可调用
  context?: 'inline' | 'fork'    // 在当前对话运行或启动子代理
  disableModelInvocation?: boolean // 是否禁止模型自动调用
}

// 捆绑技能注册
registerBundledSkill({
  name: 'simplify',
  description: 'Review changed code for reuse, quality, and efficiency',
  allowedTools: ['Read', 'Edit', 'Write', 'Grep', 'Glob'],
  userInvocable: true,
  getPromptForCommand: async (args, context) => {
    return [{ type: 'text', text: promptContent }]
  },
})
```

**两种技能加载方式**：

| 特性 | 捆绑技能 (Bundled) | 文件技能 (File) |
|------|-------------------|----------------|
| 存储位置 | 编译在代码中 | `.claude/skills/<name>/SKILL.md` |
| 注册方式 | `registerBundledSkill()` | 自动从文件系统加载 |
| 更新方式 | 需重新编译 | 修改文件即可 |
| 热重载 | 不支持 | 支持（chokidar 监听） |
| 示例 | `/simplify`, `/claude-api` | `/tutorial`, 用户自定义 |

**调用方式**：
- 用户：输入 `/技能名`
- 模型：通过 Skill 工具调用
- 文件技能支持 YAML 前置元数据配置

## 问题

1. 捆绑技能和文件技能有什么区别？各有什么优缺点？
2. 文件技能是如何实现热重载的？
3. 本教程属于哪种技能？为什么选择这种方式？

## 期望答案

1. 捆绑技能编译时包含、更新需重新编译；文件技能运行时加载、修改文件即可更新。文件技能更灵活但功能受限（纯 prompt）
2. 通过 chokidar 监听技能目录文件变化，变化后清除缓存重新加载
3. 文件技能——因为零侵入、无需编译、易分发，用户只需复制文件即可使用
