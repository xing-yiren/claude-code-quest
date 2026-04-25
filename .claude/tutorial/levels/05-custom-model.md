---
id: 5
title: 自定义模型配置
phase: 1
difficulty: 2
type: usage
skippable: true
---

## 目标

了解 Claude Code 的模型 tier 系统，学会通过 settings.json 配置自定义模型，让你的 API key 接入的模型能正常使用。

## 概念

### 什么时候需要自定义模型？

- **用自己的 API key** — 不想走 Claude Code 的计费，用你自己的 API key
- **用内置列表没有的模型** — 比如第三方模型或自部署模型
- **接入其他提供商** — 通过兼容 API 接入其他服务商

### Claude Code 的 Tier 系统

Claude Code 内部把模型分为三个 **tier（层级）**，按使用场景区分：

| Tier | 用途 | 对应变量 |
|------|------|---------|
| **Sonnet** | 日常主力，平衡速度与能力 | `ANTHROPIC_DEFAULT_SONNET_MODEL` |
| **Opus** | 复杂任务，最强推理能力 | `ANTHROPIC_DEFAULT_OPUS_MODEL` |
| **Haiku** | 快速轻量任务 | `ANTHROPIC_DEFAULT_HAIKU_MODEL` |

不同场景会自动选不同 tier（如 plan mode 切 Opus，日常用 Sonnet）。`/model` 切换的就是当前用哪个 tier。

自定义模型的核心思路是：**把你的 API 中的模型，按能力映射到这三个 tier 上**。这样 Claude Code 内部自动选 tier 时，实际调用的是你 API 里对应的模型。

### 配置方式：settings.json 的 `env` 字段

推荐通过 settings.json 的 `env` 字段配置，Claude Code 启动时自动加载。

配置文件有两个位置：

| 位置 | 作用范围 | 适合放什么 |
|------|----------|-----------|
| `C:\Users\你的用户名\.claude\settings.json` | 全局，所有项目生效 | API key、个人偏好 |
| `项目目录\.claude\settings.json` | 仅当前项目 | 项目相关的设置 |

> **安全提示**：`ANTHROPIC_BASE_URL` 和 `ANTHROPIC_AUTH_TOKEN` 只能放在**用户级** settings.json 才生效。项目级配置出于安全考虑会跳过这些变量，防止恶意项目劫持你的 API 流量。

### 配置模板

核心三要素（API 地址 + 密钥 + 模型映射）：

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "你的API地址",
    "ANTHROPIC_AUTH_TOKEN": "你的密钥",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "日常对话模型",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "复杂推理模型",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "快速响应模型"
  }
}
```

如果只有一个模型，也可以简化为 `ANTHROPIC_MODEL`（仅设默认模型，不配 tier 映射）：

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "你的API地址",
    "ANTHROPIC_AUTH_TOKEN": "你的密钥",
    "ANTHROPIC_MODEL": "模型名称"
  }
}
```

> **`modelOverrides` 的区别**：settings.json 还有一个 `modelOverrides` 字段，它是在底层全局替换 Claude Code 内部使用的规范模型 ID。env 变量控制 `/model` 选项列表，`modelOverrides` 控制底层模型引用。第三方 API 场景用 env 变量就够了。

配置好后重启 Claude Code，输入 `/model` 就能看到自定义模型出现在列表中，随时切换。

## 任务

**如果你有 API key：**
1. 打开用户级 settings.json（`C:\Users\你的用户名\.claude\settings.json`）
2. 在 `env` 字段里填入你的 API 地址、密钥和模型映射
3. 重启 Claude Code
4. 输入 `/model` 确认自定义模型出现在列表中

**如果你没有 API key：**
输入 `/tutorial skip` 跳过这一关，直接进入下一关。

## 验证

配置完成后告诉我：
- 你配了哪些 tier 映射
- `/model` 列表里能不能看到你的自定义模型

## 提示

- 不确定配什么？告诉我想用哪个提供商，我帮你写配置
- 配好 tier 后，`/model` 切换 Sonnet/Opus/Haiku 会调用你 API 里对应的模型
- 没有 API key 完全没关系，直接跳过就行
