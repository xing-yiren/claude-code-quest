---
id: 10
title: Plan Mode
phase: 1
difficulty: 2
type: usage
---

## 目标

理解 Plan Mode 的工作流，学会在复杂任务里先探索、再计划、再执行。

## 任务

Plan Mode 是 Claude Code 的一种特殊模式：Claude 会先理解代码和制定计划，不直接修改文件。你可以审查计划，满意后再让 Claude 执行。

1. 输入 `/plan` 进入 Plan Mode，或用 `Shift+Tab` 切换到 plan mode
2. 对 Claude 说："我想给这个项目添加一个 CONTRIBUTING.md 文件，包含如何贡献代码的说明"
3. 观察 Claude 如何先探索项目、再制定计划
4. 审查计划：它是否说明了要改哪些文件、为什么这么改、如何验证？
5. 如果满意就说"执行"或"继续"，让 Claude 按计划实施
6. 完成后退出 Plan Mode

完成后告诉我：Plan Mode 和普通模式有什么不同？它适合什么任务？什么任务不需要 Plan Mode？

## 验证

告诉我：

- Plan Mode 的基本流程是什么
- 它相比普通模式的优势是什么
- 哪些任务适合用 Plan Mode，哪些小任务可以直接做

## 提示

- 推荐流程是：Explore → Plan → Implement → Verify/Commit
- Plan Mode 下 Claude 不会直接修改文件，只出方案
- 适用于需求不清晰、多文件修改、架构选择、风险较高的任务
- typo、简单重命名、单行修复通常不需要 Plan Mode
- 你可以在计划阶段要求 Claude 缩小范围、补充验证方式、改实现方案
- 满意后说"执行"让 Claude 开始干活
