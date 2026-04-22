---
id: 13
title: Coordinator-Worker 架构
phase: 2
difficulty: 3
type: source
---

## 目标

理解 Claude Code 的 Coordinator-Worker 多代理架构——如何安全地协调多个 AI 代理协作。

## 背景

当 Claude Code 需要同时处理多个任务时（比如子代理），它会启动 Worker 来执行。但 Worker 不能自主批准高风险操作，需要向 Coordinator 申请审批。

## 代码节选

```typescript
// src/coordinator/coordinatorMode.ts

// Coordinator-Worker 架构：
// - Worker: 执行任务，但无权自主批准高风险操作
// - Coordinator: 持有审批权限，通过 mailbox 接收请求

// Worker 可用的工具白名单：
const INTERNAL_WORKER_TOOLS = new Set([
  'TeamCreate',     // 创建子团队
  'SendMessage',    // 向 Coordinator 通信
  'SyntheticOutput',// 合成输出
])

// Worker 请求审批的流程：
// 1. Worker 需要执行高风险操作
// 2. Worker 通过 SendMessage 向 Coordinator 发送请求
// 3. Coordinator 审查请求，批准或拒绝
// 4. Worker 根据审批结果继续执行

// 原子认领机制：
// - 防止多个 Worker 同时处理同一任务
// - 认领后其他 Worker 无法再操作
```

**关键设计点**：
- Worker 只能使用白名单中的工具
- 高风险操作（Bash、文件写入等）需要 Coordinator 审批
- 原子认领防止冲突
- 所有审批记录可审计

## 问题

1. Coordinator 和 Worker 分别负责什么职责？
2. Worker 如何向 Coordinator 请求审批？通过什么机制通信？
3. 为什么设计这个架构而不是让每个 Worker 自主决策？

## 期望答案

1. Coordinator 负责审批和协调，Worker 负责执行任务
2. 通过 mailbox 模式（SendMessage 工具）发送审批请求
3. 安全考虑——防止误操作、集中审计、统一权限控制
