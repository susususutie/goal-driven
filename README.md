# goal-driven

Goal-Driven 多智能体系统，用于持续解决具有严格成功标准的复杂问题（300+ 小时投入）。

## 安装

```bash
npx skills add susususutie/goal-driven
```

## 适用场景

编译器设计、定理证明、数据库架构、EDA 仿真等需要严密逻辑验证的高复杂度任务。

## 核心要素

| 要素 | 职责 |
|------|------|
| **Goal** | 系统最终目标，所有子智能体的唯一任务 |
| **Criteria** | 判断任务完成的条件集合（需明确、可验证） |
| **Subagent** | 持续执行任务，将大任务分解为子任务 |
| **Master Agent** | 控制者，独立评估结果，每5分钟检查活跃状态 |

## License

MIT
