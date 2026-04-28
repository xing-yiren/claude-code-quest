---
id: 21
title: 任务系统
phase: 3
difficulty: 3
type: source
---

## 目标

理解 Claude Code 的任务系统——6 种任务类型和状态机设计。

## 背景

Claude Code 内部有一个完整的任务系统，用于管理和执行不同类型的后台任务。这是实现多代理和并行操作的基础设施。

## 代码节选

```typescript
// src/Task.ts + src/tasks.ts

// 6 种任务类型
type TaskType =
  | 'LocalShell'     // 本地 shell 命令执行
  | 'LocalAgent'     // 本地子代理
  | 'RemoteAgent'    // 远程代理（sandbox 环境）
  | 'Dream'          // 后台记忆处理（AutoDream）
  | 'LocalWorkflow'  // 工作流脚本（条件编译）
  | 'MonitorMcp'     // MCP 监控工具（条件编译）

// 状态机
// pending → running → completed
//                    → failed
//                    → killed

// 任务注册
function getAllTasks(): Task[] {
  return [
    LocalShell,      // 始终可用
    LocalAgent,      // 始终可用
    RemoteAgent,     // 始终可用
    Dream,           // 始终可用
    LocalWorkflow,   // 需要 feature flag
    MonitorMcp,      // 需要 feature flag
  ]
}
```

**任务类型对比**：

| 类型 | 执行位置 | 用途 | 是否始终可用 |
|------|---------|------|------------|
| LocalShell | 本地终端 | 运行命令 | 是 |
| LocalAgent | 本地进程 | 子代理任务 | 是 |
| RemoteAgent | 远程沙箱 | 隔离执行 | 是 |
| Dream | 后台 | 记忆处理 | 是 |
| LocalWorkflow | 本地 | 工作流脚本 | 条件编译 |
| MonitorMcp | 本地 | MCP 监控 | 条件编译 |

## 问题

1. 列举至少 4 种任务类型及其执行位置和用途。
2. 任务的状态转换是怎样的？画出状态机。
3. LocalWorkflow 和 MonitorMcp 为什么是"条件编译"的？这意味着什么？

## 期望答案

1. LocalShell=本地运行命令、LocalAgent=本地子代理、RemoteAgent=远程沙箱、Dream=后台记忆处理
2. pending → running → completed/failed/killed
3. 它们用 `feature('FLAG_NAME')` 包裹，在编译时根据 feature flag 决定是否包含；意味着不是所有构建版本都有这两个任务类型
