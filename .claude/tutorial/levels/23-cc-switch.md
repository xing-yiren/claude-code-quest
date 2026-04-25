---
id: 23
title: cc-switch：多配置管理
phase: bonus
difficulty: 3
type: usage
skippable: true
---

## 目标

了解 cc-switch 这个第三方工具，学会用它管理多套 Claude Code 配置，在不同 API 提供商之间快速切换。

## 概念

### 什么是 cc-switch？

cc-switch 是社区开发的 Claude Code 配置管理工具。解决的问题是：当你有多套 API 配置（比如不同提供商的 key、不同模型组合），手动改 settings.json 很麻烦，cc-switch 让你用一条命令切换。

### 核心能力

- **多配置管理** — 保存多套 settings.json 配置，随时切换
- **快速切换** — 一条命令切到另一套配置
- **启动时切换** — 切换后直接启动 Claude Code

### 与 settings.json 的关系

cc-switch 本质上管理的就是 settings.json 的 `env` 字段组合。它的每一套配置相当于一个独立的 `env` 配置块，切换时替换 settings.json 的内容。

## 任务

（待定 — 此关为预留关卡）

## 验证

（待定）

## 提示

- cc-switch 是第三方工具，需要 `npm install -g cc-switch` 安装
- 适合有多套 API key 或需要频繁切换提供商的高级用户
- 如果只用一套配置，settings.json 就足够了，不需要 cc-switch
