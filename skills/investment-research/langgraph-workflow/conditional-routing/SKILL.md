# 条件路由 (Conditional Routing)

## Overview

条件路由是根据状态动态决定下一步执行的技能。实现智能的任务分发和流程控制。

## 何时使用

- 根据任务类型选择不同流程
- 根据分析结果决定下一步
- 实现条件分支逻辑
- 处理异常流程

## 流程

1. **条件识别**：识别需要分支的场景
2. **条件定义**：定义路由条件
3. **分支设计**：设计各分支处理逻辑
4. **默认分支**：设置默认处理
5. **路由实现**：实现路由函数
6. **测试验证**：测试各种分支情况
7. **优化**：优化路由性能

## 模板

### 条件路由模板
```python
from typing import Literal

def route_task(state: ResearchState) -> Literal["market_analyst", "industry_analyst", "company_analyst", "report"]:
    """根据任务类型和状态路由"""
    task_type = state.get("task_type")
    current_agent = state.get("current_agent")

    # 任务刚开始，确定第一个Agent
    if current_agent is None:
        if task_type == "stock":
            return "company_analyst"  # 个股研究先分析公司
        elif task_type == "industry":
            return "industry_analyst"  # 行业研究先分析行业
        elif task_type == "macro":
            return "market_analyst"  # 宏观研究先分析市场
        else:
            return "company_analyst"

    # 根据当前执行情况决定下一步
    agent_results = state.get("agent_results", [])

    # 如果还有未完成的分析，继续执行
    completed_agents = {r["agent_name"] for r in agent_results if r["status"] == "completed"}

    if "market_analyst" not in completed_agents:
        return "market_analyst"
    if "industry_analyst" not in completed_agents and task_type in ["stock", "industry"]:
        return "industry_analyst"
    if "company_analyst" not in completed_agents and task_type == "stock":
        return "company_analyst"

    # 所有分析完成，生成报告
    return "report"

# 在图中使用
graph.add_conditional_edges(
    "supervisor",
    route_task,
    {
        "market_analyst": "market_analyst",
        "industry_analyst": "industry_analyst",
        "company_analyst": "company_analyst",
        "report": "report"
    }
)
```

## 检查清单

- [ ] 条件覆盖所有情况
- [ ] 避免死循环
- [ ] 有默认分支
- [ ] 逻辑简洁清晰
- [ ] 测试覆盖完整
- [ ] 性能可接受

## 红牌警告

- 条件不完整有遗漏
- 死循环风险
- 缺少默认分支
- 条件过于复杂
- 性能问题
