# 播客研究LangGraph工作流 (Podcast Research Workflow)

## Overview

播客研究LangGraph工作流是设计多Agent协作完成播客研究的技能。

## 何时使用

- 构建播客研究系统
- 自动化研究流程
- 多播客对比研究
- 持续追踪研究

## 流程

1. **需求理解**：理解研究需求
2. **任务分解**：分解研究任务
3. **Agent设计**：设计协作Agent
4. **工作流定义**：定义工作流
5. **执行监控**：监控执行
6. **结果聚合**：聚合研究结果
7. **报告生成**：生成最终报告

## 模板

### 播客研究工作流模板
```python
from langgraph.graph import StateGraph, END
from typing import TypedDict

class PodcastResearchState(TypedDict):
    query: str
    podcasts: List[Podcast]
    episodes: List[Episode]
    transcriptions: List[Transcription]
    analysis: Analysis
    report: str

def build_podcast_research_graph():
    graph = StateGraph(PodcastResearchState)

    # 节点
    graph.add_node("search_podcasts", search_podcasts)
    graph.add_node("collect_episodes", collect_episodes)
    graph.add_node("transcribe", transcribe_episodes)
    graph.add_node("analyze", analyze_content)
    graph.add_node("generate_report", generate_report)

    # 边
    graph.add_edge("search_podcasts", "collect_episodes")
    graph.add_edge("collect_episodes", "transcribe")
    graph.add_edge("transcribe", "analyze")
    graph.add_edge("analyze", "generate_report")
    graph.add_edge("generate_report", END)

    return graph.compile()

# 并行执行优化
def transcribe_episodes(state: PodcastResearchState) -> PodcastResearchState:
    # 并行转写多个episode
    tasks = [transcribe(ep) for ep in state["episodes"]]
    transcriptions = await asyncio.gather(*tasks)
    return {"transcriptions": transcriptions}
```

## 检查清单

- [ ] 任务分解合理
- [ ] Agent协作有效
- [ ] 并行优化到位
- [ ] 错误处理完善
- [ ] 结果聚合准确
- [ ] 性能达标

## 红牌警告

- 任务分解不当
- 协作混乱
- 错误未处理
- 性能问题
- 结果丢失
