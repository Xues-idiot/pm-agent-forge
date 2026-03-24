# 评论分析 (Comment Analysis)

## Overview

评论分析是分析播客/视频下方评论的技能。包括情感分析、观点聚类、热点识别等。

## 何时使用

- 了解听众反馈
- 评估内容效果
- 发现新话题
- 舆情监控

## 流程

1. **评论采集**：采集评论数据
2. **数据清洗**：清洗评论数据
3. **情感分析**：分析情感倾向
4. **观点聚类**：聚类相似观点
5. **热点识别**：识别热点评论
6. **趋势分析**：分析评论趋势
7. **报告生成**：生成分析报告

## 模板

### 评论分析配置
```python
async def analyze_comments(video_id: str) -> CommentAnalysis:
    """分析评论"""
    # 采集评论
    comments = await collect_comments(video_id)

    # 清洗数据
    cleaned = clean_comments(comments)

    # 情感分析
    sentiments = []
    for comment in cleaned:
        sentiment = await sentiment_model.predict(comment.text)
        sentiments.append(SentimentComment(
            text=comment.text,
            sentiment=sentiment.label,
            score=sentiment.score,
            likes=comment.likes
        ))

    # 观点聚类
    clusters = cluster_opinions(comments)

    # 热点识别
    hot_comments = identify_hot_comments(comments, threshold=100)

    return CommentAnalysis(
        total_comments=len(comments),
        sentiment_distribution=calculate_distribution(sentiments),
        opinion_clusters=clusters,
        hot_comments=hot_comments,
        engagement_rate=calculate_engagement(comments)
    )
```

## 检查清单

- [ ] 评论采集完整
- [ ] 清洗有效
- [ ] 情感准确
- [ ] 聚类合理
- [ ] 热点识别
- [ ] 报告清晰

## 红牌警告

- 采集不完整
- 水军干扰
- 情感误判
- 聚类混乱
- 热点误识
