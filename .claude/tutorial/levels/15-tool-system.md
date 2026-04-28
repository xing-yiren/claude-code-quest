---
id: 15
title: 工具系统
phase: 2
difficulty: 2
type: source
---

## 目标

理解 Claude Code 的 Tool（工具）系统设计——40+ 个工具如何定义、注册和执行。

## 背景

Claude Code 的每个能力（读文件、写文件、执行命令、搜索代码等）都是一个独立的 Tool。这套系统设计精巧，值得深入学习。

## 代码节选

```typescript
// Tool 的核心类型定义 (src/Tool.ts)
type Tool = {
  name: string                    // 工具名称，如 "Read", "Bash"
  inputSchema: ToolInputJSONSchema // 输入格式（Zod v4 定义）
  permissions?: PermissionLevel    // 权限级别
  call(context, input): Promise    // 执行逻辑
}

// buildTool 工厂函数
// 为每个工具提供安全默认值
// 统一处理错误、超时、权限检查
function buildTool(config): Tool { ... }

// 工具注册中心 (src/tools.ts)
// 返回所有可用工具
function getAllTools(): Tool[] { ... }
```

**40+ 工具的分类**：

| 类别 | 工具示例 |
|------|---------|
| 文件操作 | FileReadTool, FileEditTool, FileWriteTool |
| 代码搜索 | GlobTool, GrepTool |
| 命令执行 | BashTool（9,700 行安全代码）, PowerShellTool |
| 网络 | WebFetchTool, WebSearchTool |
| 子代理 | AgentTool, SendMessageTool |
| 任务管理 | TaskCreateTool, TaskStopTool |
| 技能 | SkillTool |
| MCP | MCPTool, ListMcpResourcesTool |

**设计原则**：
- 每个工具独立文件，自包含
- 无跨工具共享可变状态
- 通过 buildTool 统一错误处理和权限检查

## 问题

1. Claude Code 有多少个工具？输入格式是用什么库定义的？
2. "无跨工具共享可变状态"这个设计原则有什么好处？
3. BashTool 为什么有 9,700 行安全代码？它在防护什么？

## 期望答案

1. 40+ 个工具，用 Zod v4 定义输入格式
2. 避免副作用、易于测试和调试、每个工具自包含、降低耦合
3. 防护命令注入、路径穿越、敏感文件访问、危险命令等安全风险
