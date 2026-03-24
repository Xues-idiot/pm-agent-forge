# LangSmith链路追踪 (LangSmith Tracing)

## Overview

LangSmith链路追踪是监控和调试投研Agent执行的技能。参考AiBuffett的LangSmith集成，追踪token消耗和执行流程。

## 何时使用

- 执行链路追踪
- Token消耗分析
- 性能瓶颈定位
- 调试Agent行为

## 流程

1. **LangSmith配置**：配置LangSmith
2. **埋点集成**：集成追踪代码
3. **执行追踪**：执行并追踪
4. **数据分析**：分析追踪数据
5. **优化**：优化瓶颈
6. **告警**：设置告警
7. **持续监控**：持续监控

## 模板

### LangSmith配置模板
```python
import os
from langchain_core.tracers.langsmith import LangSmithTracer
from langsmith import Client

# 配置环境变量
os.environ["LANGSMITH_TRACING"] = "true"
os.environ["LANGSMITH_API_KEY"] = "your_api_key"
os.environ["LANGSMITH_PROJECT"] = "investment-research"

# 使用Tracer
from langgraph.prebuilt import create_react_agent

tracer = LangSmithTracer(
    project_name="investment-research",
    example={"stock_code": "600519"}
)

agent = create_react_agent(
    model,
    tools,
    tracer=tracer
)

# 执行并查看追踪
result = agent.invoke(
    {"messages": [{"role": "user", "content": "研究贵州茅台"}]},
    config={"callbacks": [tracer]}
)

# 通过API获取追踪详情
client = Client()
runs = client.list_runs(project_name="investment-research")
for run in runs:
    print(f"Run: {run.id}, Tokens: {run.usage}")
```

## 检查清单

- [ ] 配置正确
- [ ] 埋点完整
- [ ] 数据准确
- [ ] 分析到位
- [ ] 告警有效
- [ ] 优化落地

## 红牌警告

- 配置错误无数据
- 敏感信息泄露
- 性能开销
- 数据丢失
- 告警疲劳
