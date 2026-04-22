---
id: 8
title: Plan Mode
phase: 1
difficulty: 2
type: usage
---

## 目标

理解 Plan Mode 的工作流，学会先计划后执行。

## 任务

Plan Mode 是 Claude Code 的一种特殊模式：Claude 会先制定计划，不直接修改代码。你可以审查计划，满意后再让 Claude 执行。

1. 输入 `/plan` 进入 Plan Mode
2. 对 Claude 说："我想给这个项目添加一个 CONTRIBUTING.md 文件，包含如何贡献代码的说明"
3. 观察 Claude 如何先制定计划
4. 审查计划，如果满意就说"执行"或"继续"
5. 完成后退出 Plan Mode

完成后告诉我：Plan Mode 和普通模式有什么不同？它的优势是什么？

## 验证

告诉我 Plan Mode 的工作流程和它的优势。

## 提示

- Plan Mode 下 Claude 不会直接修改文件，只出方案
- 适用于复杂任务，避免走弯路
- 你可以在计划阶段提出修改意见
- 满意后说"执行"让 Claude 开始干活
- `/plan` 再次输入可以退出 Plan Mode
