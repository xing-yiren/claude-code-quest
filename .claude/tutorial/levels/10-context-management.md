---
id: 10
title: 上下文管理
phase: 1
difficulty: 2
type: usage
---

## 目标

学会管理对话上下文，理解 `/compact` 和 `/clear` 的区别和使用时机。

## 任务

随着对话变长，消耗的 token 越来越多，响应速度和费用都会受到影响。Claude Code 提供了两种工具来管理上下文。

1. 确保你已经有了一段较长的对话（至少和 Claude 来回聊了 5 轮以上）
2. 输入 `/compact` 压缩对话上下文
3. 观察压缩后发生了什么变化
4. 了解什么时候应该用 `/compact`，什么时候应该用 `/clear`

完成后告诉我：`/compact` 和 `/clear` 的区别是什么？分别在什么场景下使用？

## 验证

告诉我 `/compact` 和 `/clear` 的区别和使用场景。

## 提示

- 长对话会消耗大量 token，影响响应速度
- `/compact` 压缩对话但保留关键信息，对用户基本透明
- `/clear` 完全清除对话历史，释放最多空间
- Claude Code 在接近上下文限制时会自动触发 AutoCompact
- 如果对话太长了，试试 `/compact` 而不是直接 `/clear`
