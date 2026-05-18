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

这一关会带你在临时目录里创建一个 Git 练习仓库，学习 `git status`、`git diff` 和本地 commit 的基本流程。

为了不污染当前项目，实操会放在 `ccq-git-practice/` 里完成。首屏只需要先做第一步，后续步骤会按进度逐步展开。

## 分步任务

下面的步骤会按顺序展开，每完成一步再进入下一步，不需要一次性看完所有命令。

### 第 1 步：检查当前目录状态

先让 Claude 检查当前目录是不是 Git 仓库：

```bash
git status
```

如果看到 `not a git repository`，说明当前目录还没有 `.git` 仓库元数据。如果已经看到分支和工作区状态，说明当前目录本身就是 Git 仓库。

完成后告诉我你看到的输出大意，再进入下一步。

### 第 2 步：创建隔离练习仓库

创建一个临时练习目录 `ccq-git-practice/`，进入它并运行：

```bash
git init
```

这个仓库只用于练习，不要在当前项目里直接 `git init`。

完成后说「继续」。

### 第 3 步：创建文件并查看 status

在练习仓库里创建一个简单文件，例如 `hello.md`，内容可以是：

```markdown
Hello Git from Claude Code Quest!
```

然后运行：

```bash
git status
```

观察 Git 如何显示未跟踪文件。完成后说「继续」。

### 第 4 步：修改文件并查看 diff

修改 `hello.md`，例如追加一行：

```markdown
This line is a Git diff practice.
```

然后运行：

```bash
git diff
```

观察 Git 如何显示具体改动。完成后说「继续」。

### 第 5 步：生成 commit message

让 Claude 根据刚才的改动给一个简短 commit message 建议。

可选：如果你想完整体验本地提交，可以让 Claude 执行本地 commit。不要 push 到远程仓库。

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
