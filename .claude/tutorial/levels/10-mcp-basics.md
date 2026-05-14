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

## 可选挑战：配置 GitHub MCP

这一节不是通过本关的必要条件。如果你暂时没有 GitHub 账号、token、组织权限，或不想配置外部服务，可以直接跳过。

如果你想动手体验一个真实 MCP，可以尝试：

1. 运行 `/mcp` 查看当前是否已有 GitHub MCP 服务器
2. 运行 `claude mcp --help` 查看当前版本支持的 MCP 配置命令
3. 按官方说明配置 GitHub MCP 服务器（通常需要 GitHub 认证或 token）
4. 再次运行 `/mcp`，确认 GitHub MCP 出现在服务器列表里
5. 让 Claude 做一个只读操作，例如查看某个仓库、Issue 或 PR 的信息

注意：GitHub MCP 更适合读取和管理 GitHub 上的对象，例如 Issue、PR、仓库元数据、评论等；本地代码提交、branch 操作、commit 和 push 仍然更适合使用 `git` / `gh` CLI，因为它们更直接、可审计，也符合 Claude Code 现有工作流。

## 验证

告诉我 2-3 个 MCP 的实际用途，并说明为什么有用。

## 提示

- MCP = Model Context Protocol，是 Anthropic 提出的开放标准
- 通过 MCP，Claude 可以读写数据库、管理 GitHub Issue/PR、调用 API 等
- MCP 服务器在 `.claude/settings.json` 或 `~/.claude/settings.json` 中配置
- 输入 `/mcp` 查看当前配置的 MCP 服务器
- GitHub MCP 是可选实操：适合 Issue/PR/仓库信息管理，不必作为本关通过条件
- 本地 commit、branch、push 更推荐继续使用 `git` / `gh` CLI
- 如果想配置某个特定工具，直接告诉 Claude，它能帮你写配置
