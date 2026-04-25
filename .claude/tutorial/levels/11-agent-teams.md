---
id: 11
title: Agent Teams：多智能体协作
phase: 1
difficulty: 4
type: usage
skippable: true
---

## 目标

了解 Claude Code 的 Agent Teams 功能，学会创建团队、生成队友，让多个 Claude Code 实例协作完成复杂任务。

## 概念

### 什么是 Agent Teams？

Agent Teams（源码中叫 Agent Swarms）是一个**实验性**多 Agent 协作功能。你可以创建一个团队，然后生成多个 Claude Code 实例作为"队友"，每个队友有独立的角色和任务，它们之间可以通过消息通信，协同完成一个大型任务。

### 典型场景

- **并行开发** — 一个队友写前端，一个队友写后端，Leader 负责协调
- **分工会审** — 一个队友写代码，一个队友做 review，另一个跑测试
- **复杂调研** — 多个队友并行搜索不同方向，汇总给 Leader

### 核心概念

| 角色 | 说明 |
|------|------|
| **Team Lead** | 团队领导者，通常是你的主 Claude Code 实例，负责分配任务和协调 |
| **Teammate** | 队友，被 Leader 生成的新 Claude Code 实例，有独立的角色和模型 |
| **Team File** | 团队状态文件，记录所有成员信息 |
| **Mailbox** | 消息信箱，队友间通过信箱收发消息 |

### 如何启用

在 settings.json 的 `env` 中设置：

```json
{
  "env": {
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
  }
}
```

或者启动时加 `--agent-teams` 参数。重启后生效。

### 核心工作流

1. **创建团队** — Claude 调用 `TeamCreate` 工具，设定团队名和目标
2. **生成队友** — Claude 调用 `Spawn` 工具，为每个队友指定角色和任务
3. **队友通信** — 队友间通过 `SendMessage` 工具收发消息，汇报进度
4. **结果汇总** — Leader 收集各队友结果，整合输出

### 队友运行方式

| 后端 | 说明 |
|------|------|
| **In-process** | 同一进程内运行，轻量快速 |
| **tmux 分屏** | 在 tmux 分屏中可视化运行，可直观看到每个队友的终端 |
| **iTerm2 原生** | macOS iTerm2 原生分屏支持 |

### 队友系统提示

每个队友启动时会收到额外提示：必须使用 `SendMessage` 工具与他人通信，直接输出文本其他队友是看不到的。

## 任务

1. 在 settings.json 中启用 `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS`
2. 重启 Claude Code
3. 告诉 Claude 你想创建一个团队来做一个任务（比如"帮我创建一个团队，分别从前后端角度分析当前项目结构"）
4. 观察 Claude 如何使用 TeamCreate 和 Spawn 工具
5. 查看底部状态栏的队友数量变化

**如果没有实验性功能权限或不想配：**
输入 `/tutorial skip` 跳过。

## 验证

完成后告诉我：
- 你创建了什么团队，生成了几个队友
- 队友之间是如何通信的
- 底部状态栏显示了什么

## 提示

- 这是实验性功能，可能需要 GrowthBook 开关授权，如果启用后仍不可用，直接跳过即可
- 队友的模型默认跟随 Leader，也可以单独指定
- 使用 `/tasks` 可以查看所有队友的运行状态
