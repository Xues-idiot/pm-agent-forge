# 并行执行 (Parallel Execution)

## Overview

并行执行是让多个Agent同时工作提升效率的技能。在LangGraph中通过Send机制实现任务的并行分发和处理。

## 何时使用

- 多个独立子任务可同时执行
- 需要加速研究流程
- 需要同时采集多源数据
- 需要并行分析多个维度

## 流程

1. **任务识别**：识别可并行的任务
2. **依赖分析**：确定任务间依赖
3. **并行设计**：设计并行执行方案
4. **结果聚合**：设计结果聚合逻辑
5. **同步控制**：处理时序和同步
6. **性能优化**：优化并行度
7. **测试验证**：验证结果正确性

## 模板

### 并行执行模板
```python
from langgraph.constants import Send
from typing import List

def parallel_analysis(state: ResearchState) -> List[Send]:
    """并行触发多个分析任务"""
    task_type = state.get("task_type")
    stock_code = state.get("stock_code")

    tasks = []

    # 市场分析总是需要
    tasks.append(Send("market_analyst", {
        **state,
        "current_agent": "market_analyst"
    }))

    # 行业分析（个股和行业研究需要）
    if task_type in ["stock", "industry"]:
        tasks.append(Send("industry_analyst", {
            **state,
            "current_agent": "industry_analyst"
        }))

    # 公司分析（只有个股研究需要）
    if task_type == "stock":
        tasks.append(Send("company_analyst", {
            **state,
            "current_agent": "company_analyst"
        }))

    return tasks

# 在图中使用
graph.add_node("parallel_analysis", parallel_analysis)
graph.add_edge("supervisor", "parallel_analysis")
graph.add_edge("parallel_analysis", "report")

# 或使用Broadcast模式
def broadcast_data_collection(state: ResearchState) -> List[Send]:
    """并行采集多源数据"""
    return [
        Send("akshare_data", {"task": "行情数据", **state}),
        Send("tushare_data", {"task": "财务数据", **state}),
        Send("eastmoney_data", {"task": "资金流", **state}),
    ]
```

## 检查清单

- [ ] 任务确实独立可并行
- [ ] 依赖关系正确处理
- [ ] 结果聚合逻辑正确
- [ ] 无竞态条件
- [ ] 并行度合理
- [ ] 错误隔离

## 红牌警告

- 任务实际有依赖却被并行
- 结果覆盖丢失
- 竞态条件
- 并行度过高资源耗尽
- 错误传播混乱
