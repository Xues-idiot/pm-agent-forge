# 话题追踪 (Topic Tracking)

## Overview

话题追踪是跨多期播客追踪特定话题的技能。支持话题趋势分析、相关概念挖掘、观点演变追踪等。

## 何时使用

- 系列话题追踪
- 行业趋势分析
- 观点演变研究
- 竞品播客监控
- 专题研究

## 流程

1. **话题定义**：定义追踪话题
2. **来源选择**：选择播客来源
3. **数据采集**：采集相关剧集
4. **话题提取**：提取话题片段
5. **趋势分析**：分析话题趋势
6. **观点聚合**：聚合观点演变
7. **报告生成**：生成追踪报告

## 模板

### 话题追踪模板
```python
class TopicTracker:
    def __init__(self):
        self.podcast_db = PodcastDatabase()
        self.topic_extractor = TopicExtractor()
        self.sentiment_tracker = SentimentTracker()

    async def track_topic(self, topic: str, sources: List[str] = None):
        """追踪话题"""
        # 1. 搜索相关剧集
        episodes = await self.podcast_db.search_by_topic(topic, sources)

        # 2. 提取话题片段
        segments = []
        for ep in episodes:
            topic_segments = await self.topic_extractor.extract(ep, topic)
            segments.extend(topic_segments)

        # 3. 时间排序
        segments.sort(key=lambda x: x.timestamp)

        # 4. 趋势分析
        trend = await self.analyze_trend(segments)

        # 5. 观点演变
        evolution = await self.track_evolution(segments)

        # 6. 关键参与人
        key_participants = await self.identify_key_participants(segments)

        return TopicTrackingReport(
            topic=topic,
            episode_count=len(episodes),
            segment_count=len(segments),
            trend=trend,
            evolution=evolution,
            key_participants=key_participants,
            timeline=self.build_timeline(segments)
        )

    async def analyze_trend(self, segments: List[TopicSegment]):
        """分析趋势"""
        # 按时间聚合
        monthly = self.aggregate_by_month(segments)
        return {
            "volume_trend": self.calculate_volume_trend(monthly),
            "sentiment_trend": self.sentiment_tracker.track(monthly),
            "emerging_subtopics": self.find_emerging(segments)
        }
```

## 检查清单

- [ ] 覆盖全面
- [ ] 提取准确
- [ ] 趋势清晰
- [ ] 报告完整

## 红牌警告

- 遗漏相关
- 提取错误
- 趋势偏差
- 报告混乱
