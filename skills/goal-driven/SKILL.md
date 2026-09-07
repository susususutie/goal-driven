---
name: goal-driven
description: Goal-Driven 多智能体系统，用于持续解决具有严格成功标准的复杂问题（300+ 小时投入）。
---

# Goal-Driven 多智能体系统

**Purpose:** 让 AI 系统能够持续投入 300+ 小时解决具有严格成功标准的复杂问题。

**适用场景:** 编译器设计、定理证明、数据库架构、EDA 仿真等需要严密逻辑验证的高复杂度任务。

## 四大核心要素

| 要素 | 职责 |
|------|------|
| **Goal** | 系统最终目标，所有子智能体的唯一任务 |
| **Criteria** | 判断任务完成的条件集合（需明确、可验证） |
| **Subagent** | 持续执行任务，将大任务分解为子任务 |
| **Master Agent** | 控制者，独立评估结果，每5分钟检查活跃状态 |

## 标准 Prompt 模板

```
# Goal-Driven(1 master agent + 1 subagent) System

Goal: [[[[[在此定义你的最终目标]]]]]

Criteria for success: [[[[[在此定义你的成功标准]]]]]

## Subagent's description:

The subagent's goal is to complete the task assigned by the master agent.
The goal defined above is the final and the only goal for the subagent.
The subagent should have the ability to break down the task into smaller sub-tasks,
and assign the sub-tasks to itself or other subagents if necessary.
The subagent should also have the ability to monitor the progress of each sub-task
and update the master agent accordingly.
The subagent should continue to work on the task until the criteria for success are met.

## Master agent's description:

The master agent is responsible for overseeing the entire process and ensuring that
the subagent is working towards the goal. The only 3 tasks that the main agent need to do are:

1. Create subagents to complete the task.
2. If the subagent finishes the task successfully or fails to complete the task,
   the master agent should evaluate the result by checking the criteria for success.
   If the criteria for success are met, the master agent should stop all subagents and end the process.
   If the criteria for success are not met, the master agent should ask the subagent
   to continue working on the task until the criteria for success are met.
3. The master agent should check the activities of each subagent for every 5 minutes,
   and if the subagent is inactive, please check if the current goal is reached and verify the status.
   If the goal is not reached, restart a new subagent with the same name to replace the inactive subagent.
   The new subagent should continue to work on the task and update the master agent accordingly.
4. This process should continue until the criteria for success are met.
   DO NOT STOP THE AGENTS UNTIL THE USER STOPS THEM MANUALLY FROM OUTSIDE.
```

## 伪代码流程

```
create a subagent to complete the goal

while (criteria are not met) {
  check the activity of the subagent every 5 minutes
  if (the subagent is inactive or declares that it has reached the goal) {
    check if the current goal is reached and verify the status
    if (criteria are not met) {
      restart a new subagent with the same name to replace the inactive subagent
    } else {
      stop all subagents and end the process
    }
  }
}
```

## 核心执行原则

1. **目标必须明确且可分解** — 能分解为可验证的子任务
2. **标准必须可判定** — Master Agent 能独立判断是否满足
3. **自动恢复机制** — Subagent 不活跃时自动重启，而非放弃
4. **持续直到手动停止** — 除非用户外部干预，否则不停止循环

## 成功案例

| 项目 | 耗时 |
|------|------|
| C++ 实现 TypeScript 编译器 | ~100小时 |
| Rust 实现 SQLite | ~30小时 |

## 注意事项

- **不要**将此 prompt 添加到 AI 插件/技能中（避免上下文污染）
- 流程会消耗大量时间和 tokens，确保 API 余额充足
- 适用于 Claude Code、Codex、OpenClaw 或任何支持多智能体的工具
