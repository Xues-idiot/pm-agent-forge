# 跨Episode分析 (Cross-Episode Analysis)

## Overview

跨Episode分析是分析同一播客多个Episode之间关系和发展脉络的技能。

## 何时使用

- 追踪播客发展
- 分析系列主题
- 了解嘉宾变化
- 构建知识图谱

## 流程

1. **数据收集**：收集多Episode数据
2. **主题追踪**：追踪主题演变
3. **嘉宾追踪**：追踪嘉宾出现
4. **观点对比**：对比观点变化
5. **时间线构建**：构建时间线
6. **趋势分析**：分析发展趋势
7. **报告生成**：生成分析报告

## 模板

### 跨Episode分析模板
```python
async def analyze_podcast_series(podcast_id: str, limit: int = 50) -> SeriesAnalysis:
    """分析播客系列"""
    # 收集episodes
    episodes = await get_episodes(podcast_id, limit=limit)

    # 主题分析
    topics_over_time = track_themes(episodes)

    # 嘉宾分析
    guest_appearances = track_guests(episodes)

    # 质量趋势
    quality_trend = analyze_quality(episodes)

    # 生成报告
    return SeriesAnalysis(
        podcast_name=episodes[0].podcast_name,
        num_episodes=len(episodes),
        topic_evolution=topics_over_time,
        guest_network=build_guest_network(guest_appearances),
        quality_trend=quality_trend,
        highlights=extract_highlights(episodes)
    )
```

## 检查清单

- [ ] 数据覆盖完整
- [ ] 分析维度全面
- [ ] 趋势判断准确
- [ ] 时间线清晰
- [ ] 报告可读
- [ ] 洞察有价值

## 红牌警告

- 数据缺失
- 分析片面
- 趋势误判
- 逻辑跳跃
- 报告混乱
