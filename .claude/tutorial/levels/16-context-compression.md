---
id: 16
title: 上下文压缩策略
phase: 2
difficulty: 3
type: source
---

## 目标

理解 Claude Code 的三层上下文压缩策略——如何在有限的上下文窗口中高效运行。

## 背景

LLM 有上下文窗口限制。Claude Code 设计了三级压缩策略，在不影响用户体验的前提下最大化利用有限的上下文空间。

## 代码节选

```typescript
// src/services/compact/ — 三层压缩策略

// 第一层：MicroCompact（本地，零 API 调用）
// 在本地编辑缓存中压缩
// 移除低价值消息（如已完成的工具调用细节）
// 立即生效，不消耗 token
function microCompact(messages): Message[] { ... }

// 第二层：AutoCompact（自动触发）
// 接近窗口上限时触发（13,000 token 缓冲区）
// 压缩对话，保留活跃文件和关键上下文
// 重新注入系统提示词
// 对用户透明
function autoCompact(messages, state): Message[] { ... }

// 第三层：Full Compact（用户手动触发）
// 通过 /compact 命令
// 压缩全部对话
// 重新注入活跃文件
// 释放最多上下文空间
function fullCompact(messages, state): Message[] { ... }
```

**三层压缩的对比**：

| 特性 | MicroCompact | AutoCompact | Full Compact |
|------|-------------|-------------|-------------|
| 触发方式 | 本地缓存满时 | 接近窗口上限 | 用户手动 |
| API 调用 | 无 | 无（本地处理） | 无 |
| 压缩程度 | 轻度 | 中度 | 深度 |
| 用户感知 | 无 | 几乎无 | 有 |
| 释放空间 | 较少 | 中等 | 最多 |

## 问题

1. 三种压缩策略的触发条件分别是什么？
2. MicroCompact 为什么是"零 API 调用"的？它是怎么工作的？
3. AutoCompact 压缩后做了什么来确保模型能继续正常工作？

## 期望答案

1. MicroCompact=本地编辑缓存积累到阈值、AutoCompact=接近窗口上限（13,000 token 缓冲区）、Full Compact=用户输入 /compact
2. 在本地内存中操作，不调用 LLM API；通过移除低价值消息来压缩
3. 重新注入系统提示词和活跃文件，确保模型有完整的上下文继续工作
