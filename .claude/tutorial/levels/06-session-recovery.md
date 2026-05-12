---
id: 6
title: 会话管理：标记、查看、新建与恢复
phase: 1
difficulty: 2
type: usage
skippable: true
---

## 目标

通过一次完整演练，掌握 Claude Code 的 session 生命周期：如何给当前会话做标记、如何在 `/resume` 中查看和管理历史会话、如何用 `/clear` / `/new` 开始一个干净会话，以及如何恢复回之前的会话。

本关重点是验证：**`/clear` / `/new` 会开始一个新会话，但旧 session 仍然可以通过历史记录找回。**

## 概念

### 什么是 session？

Claude Code 的一次连续对话就是一个 **session**。每个 session 都会保存自己的对话历史、标题和相关上下文，方便你之后继续。

### 给 session 做标记：`/rename`

为了在 `/resume` 里更容易找到某个会话，可以先给它起一个明确的标题。

例如：

- `/rename ccq-l6-before-clear`
- `/rename ccq-l6-after-clear`

这样你之后在历史列表里就更容易搜索和辨认它们。

### 查看历史会话：`/resume`

`/resume` 会打开历史会话选择器。你可以在里面：

- 搜索历史 session
- 预览会话内容
- 恢复到某个旧 session
- 按当前版本支持情况，对 session 重命名或切换过滤视图

不同版本界面提示可能略有差异，请以你当前界面底部显示的快捷键提示为准。

### 新建干净会话：`/clear` 或 `/new`

- `/clear`：清空当前上下文并开始一个新的 session
- `/new`：`/clear` 的别名

重点：它们会让你进入一个新的干净会话，旧 session 仍然可以从历史记录中找回。

### 当前会话内回退：rewind

rewind 不是 `/rewind` 命令，而是当前 session 内的回退能力。它和 `/resume` 不一样：

- `/resume`：切换到历史 session
- rewind：在**当前** session 内回到较早节点重新尝试

## 任务

请按顺序完成下面这次演练：

1. 先给当前 session 命名：
   - 输入 `/rename ccq-l6-before-clear`

2. 打开历史会话选择器：
   - 输入 `/resume`
   - 观察历史 session 列表
   - 尝试搜索 `ccq-l6-before-clear`
   - 按你当前版本界面提示，尝试一些管理操作，例如：
     - 查看所有 projects 的会话
     - 按当前 branch 或 worktree 过滤
     - 预览某个会话
     - 重命名某个历史会话
   - 观察界面里还有哪些额外管理选项

3. 取消 `/resume` 后，开始一个新的干净 session：
   - 输入 `/clear` 或 `/new`

4. 在新的 session 里再次命名：
   - 输入 `/rename ccq-l6-after-clear`

5. 再次打开历史会话：
   - 输入 `/resume`
   - 搜索并恢复 `ccq-l6-before-clear`

6. 恢复成功后，在那个旧 session 里发一条消息：
   - `我已恢复到 ccq-l6-before-clear`

7. 如果你愿意，再额外体验一次 rewind，感受它和 `/resume` 的区别

## 完成后告诉我

- `/clear` / `/new` 做了什么？
- `/clear` 之后，旧 session 还能不能找回？
- `/resume` 除了恢复会话，你还看到了哪些管理能力？
- `/resume` 除了恢复会话，你还看到了哪些管理能力？
- rewind 和 `/resume` 最大的区别是什么？

## 验证

本关通过标准：

- 你成功把当前 session 命名为 `ccq-l6-before-clear`
- 你在 `/clear` 之后又创建了一个新的 session，并命名为 `ccq-l6-after-clear`
- 你能通过 `/resume` 恢复回 `ccq-l6-before-clear`
- 你能说明 `/clear`、`/resume`、rewind 三者的区别

## 提示

- `/rename` 用来给 session 打标签，方便之后搜索
- `/resume` 解决的是“我想回到以前的会话”
- `/clear` / `/new` 解决的是“我想开始一个新的干净会话”
- rewind 解决的是“当前这条对话走错了，我想在同一个 session 里回到前面的节点重试”
- `/clear` / `/new` 后，旧 session 仍然可以通过 `/resume` 找回
