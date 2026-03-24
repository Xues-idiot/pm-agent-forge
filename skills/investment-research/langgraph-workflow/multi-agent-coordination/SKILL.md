# 多Agent协调 (Multi-Agent Coordination)

## Overview

多Agent协调是设计多个专业Agent协作完成复杂任务的技能。基于LangGraph的状态机和工作流机制，实现Agent间的高效协作。

## 何时使用

- 复杂投研任务需要多专业协作
- 需要并行执行多个子任务
- 需要汇总多方分析结果
- 需要条件分支和动态路由

## 流程

1. **任务分解**：将大任务分解为子任务
2. **Agent定义**：定义各子Agent的角色和能力
3. **状态设计**：设计共享状态结构
4. **路由设计**：设计任务路由逻辑
5. **结果聚合**：聚合各Agent返回结果
6. **条件判断**：实现条件分支逻辑
7. **错误处理**：处理Agent执行异常

## 模板

### LangGraph多Agent架构模板
```python
from langgraph.graph import StateGraph, END
from typing import TypedDict, List

# 定义状态
class ResearchState(TypedDict):
    task: str
    stock_code: str
    market_analysis: dict
    industry_analysis: dict
    company_analysis: dict
    report: str
    error: str

# 定义节点
def market_analyst_node(state: ResearchState) -> ResearchState:
    """宏观/市场分析师"""
    result = analyze_market(state)
    return {"market_analysis": result}

def industry_analyst_node(state: ResearchState) -> ResearchState:
    """行业分析师"""
    result = analyze_industry(state)
    return {"industry_analysis": result}

def company_analyst_node(state: ResearchState) -> ResearchState:
    """公司分析师"""
    result = analyze_company(state)
    return {"company_analysis": result}

def report_node(state: ResearchState) -> ResearchState:
    """报告生成"""
    report = generate_report(state)
    return {"report": report}

# 构建图
graph = StateGraph(ResearchState)
graph.add_node("market_analyst", market_analyst_node)
graph.add_node("industry_analyst", industry_analyst_node)
graph.add_node("company_analyst", company_analyst_node)
graph.add_node("report", report_node)

# 定义边
graph.add_edge("market_analyst", "report")
graph.add_edge("industry_analyst", "report")
graph.add_edge("company_analyst", "report")
graph.add_edge("report", END)

# 编译
app = graph.compile()
```

## 检查清单

- [ ] 状态结构设计合理
- [ ] Agent职责划分清晰
- [ ] 路由逻辑正确
- [ ] 并行执行优化到位
- [ ] 错误处理完善
- [ ] 结果聚合逻辑正确

## 红牌警告

- 状态过于复杂难维护
- Agent间依赖关系混乱
- 缺少超时机制
- 状态更新丢失
- 无限循环风险
