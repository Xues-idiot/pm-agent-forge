# 状态管理 (State Management)

## Overview

状态管理是在LangGraph中设计和管理共享状态的技能。确保多Agent协作时数据一致性和正确流转。

## 何时使用

- 多Agent共享数据
- 需要跟踪任务进度
- 需要条件分支判断
- 需要历史记录追溯

## 流程

1. **状态设计**：定义状态结构
2. **字段定义**：定义各字段类型和用途
3. **默认值**：设置默认值
4. **更新规则**：定义状态更新逻辑
5. **并发控制**：处理并发更新
6. **持久化**：设计状态持久化
7. **监控**：状态变更监控

## 模板

### 状态定义模板
```python
from typing import TypedDict, Optional, List
from pydantic import BaseModel, Field
from datetime import datetime
from enum import Enum

class TaskStatus(str, Enum):
    PENDING = "pending"
    IN_PROGRESS = "in_progress"
    COMPLETED = "completed"
    FAILED = "failed"

class AgentResult(BaseModel):
    agent_name: str
    result: dict
    timestamp: datetime
    status: TaskStatus
    error: Optional[str] = None

class ResearchState(TypedDict):
    # 任务信息
    task_id: str
    task_type: str  # stock/industry/macro
    status: TaskStatus

    # 输入
    stock_code: Optional[str]
    industry: Optional[str]

    # 分析结果
    market_analysis: Optional[dict]
    industry_analysis: Optional[dict]
    company_analysis: Optional[dict]

    # 中间结果
    raw_data: Optional[dict]
    processed_data: Optional[dict]

    # 最终结果
    report: Optional[str]
    investment_advice: Optional[str]

    # 执行追踪
    agent_results: List[AgentResult]
    current_agent: Optional[str]
    error: Optional[str]

# 默认值工厂
def default_state() -> ResearchState:
    return {
        "task_id": "",
        "task_type": "stock",
        "status": TaskStatus.PENDING,
        "agent_results": [],
    }
```

## 检查清单

- [ ] 状态结构完整
- [ ] 字段类型正确
- [ ] 默认值合理
- [ ] 更新逻辑清晰
- [ ] 并发安全
- [ ] 可追溯

## 红牌警告

- 状态过于庞大
- 缺少必要字段
- 并发更新冲突
- 状态丢失
- 敏感信息暴露
