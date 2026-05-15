---
id: 4
title: Git 工作流基础
phase: 1
difficulty: 1
type: usage
---

## 目标

学会让 Claude Code 安全地使用 Git 查看、解释和保存本地改动。

## 任务

Claude Code 可以帮你使用 Git，但 Git 命令必须在一个 Git 仓库里运行。为了不污染当前项目，这一关会在临时练习目录里完成。

1. 先让 Claude 检查当前目录是不是 Git 仓库：
   ```bash
   git status
   ```
2. 如果看到 `not a git repository`，理解它表示当前目录还没有 `.git` 仓库元数据
3. 创建一个临时练习目录 `ccq-git-practice/`
4. 在练习目录里运行 `git init`
5. 创建一个简单文件，例如 `hello.md`
6. 让 Claude 解释 `git status` 的输出
7. 修改 `hello.md`，再让 Claude 解释 `git diff` 的输出
8. 让 Claude 给出一个 commit message 建议
9. 可选：让 Claude 创建本地 commit
10. 不要 push 到远程仓库

完成后告诉我：`git status`、`git diff`、`git commit` 分别做什么？为什么 `push` / PR 比本地 Git 操作更敏感？

## 验证

告诉我：

- `git status` 显示什么信息
- `git diff` 显示什么信息
- commit 的作用是什么
- 为什么 push / PR 需要额外确认

## 提示

- Git 仓库通常包含一个 `.git/` 目录
- `git status` 用来查看当前工作区有哪些改动
- `git diff` 用来查看具体改了哪些内容
- commit 是把本地改动保存成一个历史快照
- push 会把本地提交发送到远程仓库，对别人可见，所以需要更谨慎
- 练习请放在 `ccq-git-practice/`，不要在当前项目里直接 `git init`
