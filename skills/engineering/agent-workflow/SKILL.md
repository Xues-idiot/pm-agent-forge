---
name: engineering-agent-workflow
description: Use when designing AI agent workflows, architecting multi-agent systems, or solving problems with agentic approaches. Based on Meta's 9-step agent building process.
---

# Agent Workflow Design

设计AI Agent工作流和架构多Agent系统。

## 何时使用

- 设计新的AI Agent
- 改进现有Agent
- 解决多Agent协作问题
- 集成外部工具到Agent架构
- 业务问题转化为Agent方案

## 工作流决策树

```
收到问题
    ↓
1. 问题是否清晰？
   ├─ 否 → 澄清问题
   └─ 是 → 继续
    ↓
2. 复杂度如何？
   ├─ 简单（单一任务）→ 单Agent + 基础工具
   ├─ 复杂（多子任务）→ 多Agent编排
   └─ 集成（系统连接）→ 聚焦工具层设计
    ↓
3. 选择工作流
   ├─ 新Agent → 9步构建法
   ├─ 改进现有 → 聚焦特定层
   └─ 工具集成 → MCP模式
```

## 9步Agent构建法

> 来自Meta验证的方法论

### Step 1: 定义目的和范围

**核心原则：** 从Job-to-be-done出发，不是从技术出发

**必问问题：**
- 终端用户需要什么具体结果？
- 约束条件是什么（预算、时间、资源）？
- 成功指标是什么？

**好/坏范围对比：**

| 坏 | 好 |
|----|----|
| "客户服务的AI助手" | "接收客户投诉，从Shopify拉取订单，起草$200以下退款审批" |

**决策点：** 范围越窄 = 表现越好。避免瑞士军刀。

### Step 2: 结构化输入输出

**把Agent当作函数设计：**

```json
// 输入 - 使用JSON Schema/Pydantic
Input: {
  "complaint_text": "string (required)",
  "customer_id": "string (required)",
  "order_id": "string (optional)"
}

// 输出 - 返回数据对象不是散文
Output: {
  "action": "approve_refund | escalate | request_info",
  "refund_amount": "number",
  "reasoning": "string",
  "confidence": "number (0-1)"
}
```

### Step 3: 编写System Instructions

**关键：** 80%设计时间花在这里

System Prompt应该包含：
- **Role定义**："You are a sales qualification specialist..."
- **行为准则**："Always ask for budget before proposing solutions"
- **输出格式**："Return JSON with fields X, Y, Z"
- **边界处理**："When data is missing, return error code E001"

**经验：** 好的System Prompt可以让GPT-3.5胜过差Prompt的GPT-4。

### Step 4: 启用推理和外部动作

**ReAct框架：**
```
Reason → Act → Observe → Reason...
1. Reason: 分析当前状态，决定下一步
2. Act: 调用API、使用工具、做决策
3. Observe: 审查结果，判断目标是否达成
```

**从简单开始：**
```
Level 1: 单一Prompt（最简单）
Level 2: Prompt + 单一工具
Level 3: Prompt + 多个工具
Level 4: 多Agent协作
```

### Step 5: 定义Agent角色

**角色定义模板：**
```markdown
## Agent: [名称]

### 职责
[一句话描述核心职责]

### 边界
- 负责：[范围内的事]
- 不负责：[范围外的事]

### 决策权限
- 可以独立决定：[列出]
- 需要升级：[列出]

### 输入
[Agent接受的输入类型]

### 输出
[Agent产生的输出类型]
```

### Step 6: 设计状态管理

**状态设计问题：**
- Agent需要记住什么？
- 状态存储在哪里？（内存/DB/文件）
- 状态生命周期多长？
- 并发访问如何处理？

```python
# 状态管理示例
class AgentState:
    def __init__(self):
        self.conversation_history: List[Message] = []
        self.user_context: Dict[str, Any] = {}
        self.agent_memory: Dict[str, Any] = {}
        self.tool_results: Dict[str, Any] = {}

    def reset(self):
        """重置但保留关键上下文"""
        self.conversation_history = []
        self.tool_results = {}
```

### Step 7: 设计错误处理

**错误处理层次：**
```
用户输入验证
    ↓ (无效输入)
返回友好错误消息
    ↓ (有效输入)
Agent执行
    ↓ (执行失败)
降级策略
    ↓ (完全失败)
人工介入
```

```python
# 降级策略示例
def execute_with_fallback(agent, user_input):
    try:
        return agent.execute(user_input)
    except ValidationError as e:
        return {"error": "INVALID_INPUT", "message": str(e)}
    except ToolUnavailableError:
        return agent.execute_simplified(user_input)  # 降级
    except AgentError:
        return {"error": "AGENT_ERROR", "escalate": True}
```

### Step 8: 设计工具接口

**工具设计原则：**
- 单一职责
- 有清晰的输入输出
- 幂等操作（可安全重试）
- 超时处理

```python
# 好的工具设计
class GetOrderTool:
    name = "get_order"
    description = "获取订单详情"

    def execute(self, order_id: str, include_items: bool = False) -> dict:
        """获取订单

        Args:
            order_id: 订单ID
            include_items: 是否包含订单项

        Returns:
            包含订单信息的字典

        Raises:
            OrderNotFoundError: 订单不存在时
        """
        order = Order.objects.get(id=order_id)
        result = order.to_dict()
        if include_items:
            result['items'] = [item.to_dict() for item in order.items]
        return result
```

### Step 9: 定义Agent间通信

**多Agent通信模式：**

| 模式 | 适用场景 | 示例 |
|------|----------|------|
| Sequential | 有依赖的任务链 | 用户分层→触达内容→效果追踪 |
| Parallel | 独立任务 | 同时查询多个数据源 |
| Hierarchical | Supervisor模式 | Supervisor分解任务给子Agent |
| Fan-out | 批量任务 | 向所有用户发送通知 |

```python
# Sequential模式
from langgraph.graph import StateGraph

workflow = StateGraph(AgentState)
workflow.add_node("segmentation", segmentation_agent)
workflow.add_node("outreach", outreach_agent)
workflow.add_node("tracking", tracking_agent)

workflow.add_edge("segmentation", "outreach")
workflow.add_edge("outreach", "tracking")

# Parallel模式
results = await asyncio.gather(
    agent1.execute(task1),
    agent2.execute(task2),
    agent3.execute(task3)
)
```

## Agent设计模板

```markdown
# Agent设计方案

## 基本信息
- **名称**: [Agent名称]
- **版本**: v1.0
- **日期**: YYYY-MM-DD
- **状态**: 设计中/开发中/已上线

## 目标
[一句话描述Agent要完成什么]

## 范围
### 负责
- [具体职责1]
- [具体职责2]

### 不负责
- [明确边界]

## 输入
| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| | | | |

## 输出
| 字段 | 类型 | 说明 |
|------|------|------|
| | | |

## System Prompt
```
[完整的System Prompt]
```

## 工具
| 工具 | 用途 | 调用方式 |
|------|------|----------|
| | | |

## 状态管理
[状态设计说明]

## 错误处理
[错误处理策略]

## 评估指标
- [指标1]
- [指标2]
```

## 检查清单

- [ ] 目的和范围清晰
- [ ] 输入输出结构化
- [ ] System Prompt详细
- [ ] 工具接口清晰
- [ ] 状态管理设计
- [ ] 错误处理完备
- [ ] Agent通信定义
- [ ] 评估指标明确

## 红牌警告

- 范围太大（瑞士军刀）
- 输入输出无结构
- System Prompt空洞
- 无错误处理
- 假设Agent有完美上下文
- 不考虑成本和延迟

## 好/坏对比

**好设计：**
```
Agent: 退款审批Agent
范围: 接收投诉→拉取订单→起草$200以下退款审批
输入: {complaint_text, customer_id, order_id}
输出: {action, refund_amount, reasoning, confidence}
System Prompt: 20+行详细指令
工具: get_order(id), get_customer(id), approve_refund(amount)
```

**坏设计：**
```
Agent: 客服Agent
范围: 帮忙解决客户问题
输入: 客户消息
输出: 回复
（太模糊，无法评估和改进）
```
