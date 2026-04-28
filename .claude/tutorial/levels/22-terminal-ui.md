---
id: 22
title: 终端 UI
phase: 3
difficulty: 2
type: source
---

## 目标

理解 Claude Code 的终端 UI 渲染技术——React + Ink 如何工作。

## 背景

Claude Code 的终端界面是用 React 渲染的。它使用 Ink——一个将 React 组件渲染到终端的库。这就是为什么你能看到格式化的文本、进度条、彩色输出等。

## 代码节选

```
技术栈：
- React          ← UI 组件框架
- Ink            ← 终端 React 渲染器

核心 Ink 组件：
  App.tsx        → 应用根组件
  Box.tsx        → 布局容器（类似 div）
  Text.tsx       → 文本渲染（支持颜色、样式）
  Newline.tsx    → 换行
  Spacer.tsx     → 间距
  Button.tsx     → 按钮

业务组件：
  Markdown.tsx       → Markdown 渲染
  ProgressBar.tsx    → 进度条
  ToolUseLoader.tsx  → 工具调用动画
  Dialog.tsx         → 对话框
  CustomSelect/      → 自定义选择器
  CompactSummary.tsx → 压缩摘要
  AgentProgressLine  → 代理进度

渲染原理：
  Ink 将 React 虚拟 DOM 转换为终端字符输出
  每次状态更新 → 重新渲染 → 更新终端显示
  支持流式更新（打字机效果）
```

## 问题

1. Claude Code 使用什么技术栈来渲染终端界面？
2. Ink 和 React 是什么关系？Ink 做了什么？
3. 为什么选择 Ink 而不是其他终端 UI 框架（如 blessed）？

## 期望答案

1. React + Ink
2. Ink 是一个终端 React 渲染器——它把 React 组件渲染成终端字符输出，而不是 DOM
3. 利用 React 生态（组件化、状态管理）、支持流式渲染、轻量高效、React 开发者友好
