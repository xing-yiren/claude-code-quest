---
id: 6
title: 会话管理：标记、查看、新建、回退与恢复
phase: 1
difficulty: 2
type: usage
skippable: true
---

## 目标

完成一次完整的 session 管理演练：标记当前会话，查看 `/resume` 历史列表，体验 `/rewind` 在当前 session 内回退，再用 `/clear` / `/new` 新开一个干净 session，最后从新 session 里恢复回原来的 session。

你会验证三件事：

- `/resume` 用来切换到历史 session
- `/rewind` 用来回到当前 session 内的早期消息
- `/clear` / `/new` 会开启一个新的 session，但旧 session 仍然可以找回

## 速记

- `/rename <name>`：给当前 session 起标题，方便之后搜索
- `/resume`：查看并恢复历史 session
- `/rewind`：在当前 session 内选择一个较早节点回退
- `/clear` / `/new`：开始一个新的干净 session

## 快捷键指南

在 `/resume` 里，以你当前界面底部提示为准。常见操作包括：

| 操作 | 作用 |
|------|------|
| `/` | 搜索 session |
| `Space` | 预览选中的 session |
| `Enter` | 恢复选中的 session |
| `Esc` | 退出列表 |
| `Ctrl+A` | 切换当前 project / 所有 projects 的 session 视图 |
| `Ctrl+B` | 按当前 branch 过滤，如果当前版本支持 |
| `Ctrl+R` | 重命名历史 session，如果当前版本支持 |

在 `/rewind` 里，通常用方向键或 `j` / `k` 选择消息，用 `Enter` 确认，`Esc` 取消；仍然以界面底部提示为准。

## 这关怎么做

这关请一次做完整个流程，**中途不用反复回来输入 `/tutorial`**。等你已经恢复回旧 session 后，再回来验证即可。

## 闯关任务

### 1. 给当前 session 打标记

输入：

```text
/rename ccq-l6-before-clear
```

### 2. 打开 `/resume` 看看

输入：

```text
/resume
```

请观察并尝试：

- 用 `/` 搜索 session
- 用 `Space` 预览一个 session
- 看看底部是否还有 all projects、branch filter、rename 等快捷键

注意：当前正在使用的 session 不会出现在可恢复列表里，所以这一步搜不到 `ccq-l6-before-clear` 是正常的。观察完后退出 `/resume`，不要恢复别的 session。

### 3. 体验当前 session 内回退

输入：

```text
/rewind
```

打开选择器后，只需要观察它列出的当前 session 消息，并确认它是在当前 session 内选择回退点。为了不影响后面的验证，建议按 `Esc` 取消退出。

### 4. 开一个新的干净 session

输入其中一个：

```text
/clear
```

或：

```text
/new
```

### 5. 你现在已经在新 session 里了

继续在**这个新 session**里完成后面的步骤，不需要先回旧 session。

先输入：

```text
/rename ccq-l6-after-clear
```

然后再次打开：

```text
/resume
```

搜索并恢复：

```text
ccq-l6-before-clear
```

### 6. 恢复成功后，留一句标记

恢复回旧 session 后，发送：

```text
我已恢复到 ccq-l6-before-clear
```

## 完成后回复我

请用短句回答这 3 个问题：

1. 哪个命令会开启一个新的干净 session？
2. `/resume` 和 `/rewind` 分别是在什么范围内切换？
3. `/clear` 之后，旧 session 还能不能通过 `/resume` 找回？

## 验证

本关通过标准：

- 出现过 `ccq-l6-before-clear` 和 `ccq-l6-after-clear` 两个 session 标题
- 两个标题属于不同 session
- 你恢复回 `ccq-l6-before-clear` 后发送了指定消息
- 你能用简短的话说明 `/clear`、`/resume`、`/rewind` 的区别

## 提示

如果你在第一次 `/resume` 里找不到当前 session，别慌：这是正常行为。先 `/clear` 或 `/new` 进入新 session 后，旧 session 才会出现在可恢复列表里。
