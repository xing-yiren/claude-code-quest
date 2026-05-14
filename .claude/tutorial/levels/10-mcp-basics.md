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

下面是一条适合教学场景的安全路线：先配置 **只读 GitHub MCP**，确认能读取仓库/Issue/PR，再决定是否开放写权限。

### 准备条件

1. 安装并启动 Docker
2. 准备一个 GitHub Personal Access Token
   - 建议用 fine-grained token，只授权一个测试仓库
   - 起步只给只读权限，例如 Metadata / Contents / Issues / Pull requests 的 read 权限
   - 如果之后确实要让 MCP 创建 issue/comment/PR，再单独增加对应写权限
3. 不要把 token 写进项目文件或提交到仓库

### 配置步骤

1. 先查看当前版本的 MCP 命令：

```bash
claude mcp --help
claude mcp add --help
```

2. 添加 GitHub MCP 服务器（用户级配置）：

```bash
claude mcp add -s user \
  -e GITHUB_PERSONAL_ACCESS_TOKEN=你的_GitHub_Token \
  -e GITHUB_READ_ONLY=1 \
  github -- \
  docker run -i --rm \
    -e GITHUB_PERSONAL_ACCESS_TOKEN \
    -e GITHUB_READ_ONLY \
    ghcr.io/github/github-mcp-server
```

说明：
- `-s user` 表示把 MCP 配置放到用户级，换项目也能用
- `GITHUB_READ_ONLY=1` 表示先用只读模式，降低误操作风险
- `docker run ... ghcr.io/github/github-mcp-server` 会启动 GitHub 官方 MCP server

3. 验证配置：

```bash
claude mcp list
```

然后回到 Claude Code，运行：

```text
/mcp
```

确认列表里能看到 `github`。

4. 做一个只读测试：

让 Claude 通过 GitHub MCP 查看某个测试仓库、Issue 或 PR 的信息。例如：

```text
用 GitHub MCP 查看我的 <owner>/<repo> 仓库信息
```

### 和 git / gh CLI 的边界

GitHub MCP 更适合读取和管理 GitHub 上的对象，例如 Issue、PR、仓库元数据、评论等。本地代码提交、branch 操作、commit 和 push 仍然更适合使用 `git` / `gh` CLI，因为它们更直接、可审计，也符合 Claude Code 现有工作流。

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
