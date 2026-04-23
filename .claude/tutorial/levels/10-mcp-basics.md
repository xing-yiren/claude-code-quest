---
id: 10
title: MCP 扩展
phase: 1
difficulty: 2
type: usage
---

## 目标

了解 MCP（Model Context Protocol），学会配置和使用 MCP 服务器。

## 任务

MCP 是 Claude Code 的扩展协议，让 Claude 可以连接外部工具和服务——比如数据库、GitHub、文件系统等。

1. 输入 `/mcp` 查看 MCP 相关命令
2. 了解 MCP 服务器是如何配置的（在 settings.json 中）
3. 思考一下：如果给 Claude Code 连接一个 GitHub MCP 服务器，能做什么？连接一个数据库呢？

完成后告诉我：你觉得 MCP 能用来做什么？列举 2-3 个实际应用场景。

## 验证

告诉我 2-3 个 MCP 的实际用途，并说明为什么有用。

## 提示

- MCP = Model Context Protocol，是 Anthropic 提出的开放标准
- 通过 MCP，Claude 可以读写数据库、管理 GitHub Issue/PR、调用 API 等
- MCP 服务器在 `.claude/settings.json` 或 `~/.claude/settings.json` 中配置
- 输入 `/mcp` 查看当前配置的 MCP 服务器
- 如果想配置某个特定工具，直接告诉 Claude，它能帮你写配置
