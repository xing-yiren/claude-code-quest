---
id: 11
title: QueryEngine 核心引擎
phase: 2
difficulty: 2
type: source
---

## 目标

理解 Claude Code 最核心的模块——QueryEngine 的工作原理。

## 背景

QueryEngine（约 46,000 行）是 Claude Code 的中枢神经系统。它负责所有 LLM API 调用、流式传输、缓存管理、速率限制和上下文预算控制。

## 代码节选

以下是 QueryEngine 的核心结构和关键机制的简化示意：

```typescript
// QueryEngine 的核心职责
class QueryEngine {
  // 1. LLM 调用循环
  async query(messages, tools) {
    // 发送请求到 Anthropic API
    // 流式处理响应
    // 处理工具调用
    // 循环直到得到最终响应
  }

  // 2. 自动压缩机制
  // 当 已用 token + 预估响应 > 窗口上限 - 13,000 时触发
  maybeAutoCompact() {
    if (this.isNearWindowLimit(13000)) {
      // 压缩对话，保留关键上下文
      // 重新注入系统提示词
    }
  }

  // 3. 缓存管理
  // 在系统提示词和工具定义上设置 cache_control 标记
  // 利用 Anthropic API 的 Prompt Caching 功能
}
```

QueryEngine 的关键特性：
- **自愈循环**：遇到 API 错误自动重试
- **上下文预算管理**：持续追踪 token 用量
- **自动压缩**：接近窗口上限时自动触发
- **缓存优化**：利用 Prompt Caching 减少延迟和成本

## 问题

1. QueryEngine 自动压缩的触发条件是什么？预留多少 token 作为缓冲区？
2. QueryEngine 利用了什么 API 功能来优化重复调用的性能？
3. AutoCompact 和 Full Compact（用户手动触发）有什么区别？

## 期望答案

1. 当已用 token 接近窗口上限时触发，预留 13,000 token 缓冲区
2. Anthropic API 的 Prompt Caching（通过 cache_control 参数）
3. AutoCompact 是自动触发的，对用户透明；Full Compact 是用户通过 `/compact` 手动触发的完整压缩
