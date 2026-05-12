---
id: 6
title: 会话管理：标记、查看、新建与恢复
phase: 1
difficulty: 2
type: usage
skippable: true
---

## 目标

完成一次 session 生命周期演练：给当前会话打标记，查看 `/resume` 历史列表，用 `/clear` / `/new` 开一个干净会话，再恢复回原来的会话。

你会验证一件事：**`/clear` / `/new` 会开启新 session，但旧 session 仍然可以通过 `/resume` 找回。**

## 速记

- `/rename <name>`：给当前 session 起标题，方便之后搜索
- `/resume`：查看并恢复历史 session
- `/clear` / `/new`：开始一个新的干净 session
- rewind：在当前 session 内回到较早节点，不是切换到另一个 session

## 闯关任务

### 1. 标记当前 session

输入：

```text
/rename ccq-l6-before-clear
```

### 2. 先熟悉 `/resume`

输入：

```text
/resume
```

观察历史列表和底部快捷键提示。注意：当前正在使用的 session 不会出现在 `/resume` 可恢复列表里，所以这一步搜不到 `ccq-l6-before-clear` 是正常的。

建议试一下这些操作（以你的界面提示为准）：

| 快捷键 | 作用 |
|--------|------|
| `/` | 搜索 session |
| `Ctrl+A` | 切换所有 projects 的会话 |
| `Ctrl+B` | 按当前 branch 过滤 |
| `Ctrl+W` | 切换 worktree 视图/过滤 |
| `Ctrl+V` | 预览会话 |
| `Ctrl+R` | 重命名历史会话 |

试完后取消 `/resume`。

### 3. 新建干净 session

输入其中一个：

```text
/clear
```

或：

```text
/new
```

### 4. 标记新 session

输入：

```text
/rename ccq-l6-after-clear
```

### 5. 恢复旧 session

再次输入：

```text
/resume
```

这次搜索并恢复：

```text
ccq-l6-before-clear
```

恢复后发送：

```text
我已恢复到 ccq-l6-before-clear
```

## 完成后告诉我

- `/clear` / `/new` 做了什么？
- `/clear` 之后，旧 session 还能不能找回？
- `/resume` 里你试了哪些快捷键？分别有什么作用？
- rewind 和 `/resume` 最大的区别是什么？

## 验证

本关通过标准：

- 出现过 `ccq-l6-before-clear` 和 `ccq-l6-after-clear` 两个 session 标题
- 两个标题属于不同 session
- 你恢复回 `ccq-l6-before-clear` 后发送了指定消息
- 你能说明 `/clear`、`/resume`、rewind 的区别

## 提示

如果你在 `/resume` 里找不到当前 session，别慌：这是正常行为。先 `/clear` 或 `/new` 进入新 session 后，旧 session 才会出现在可恢复列表里。
