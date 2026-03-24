# 情感分析 (Sentiment Analysis)

## Overview

情感分析是分析播客内容和评论情感倾向的技能。

## 何时使用

- 了解听众反馈
- 分析内容情绪
- 评估话题热度
- 舆情监控

## 流程

1. **内容准备**：准备分析文本
2. **情感识别**：识别情感倾向
3. **强度分析**：分析情感强度
4. **观点提取**：提取情感观点
5. **趋势分析**：分析情感趋势
6. **可视化**：可视化结果
7. **报告生成**：生成分析报告

## 模板

### 情感分析模板
```python
async def analyze_sentiment(transcription: Transcription) -> SentimentAnalysis:
    """分析情感"""
    # 段落级情感
    paragraph_sentiments = []
    for para in transcription.paragraphs:
        sentiment = await sentiment_model.predict(para.text)
        paragraph_sentiments.append(SentimentSegment(
            text=para.text,
            sentiment=sentiment.label,
            score=sentiment.score,
            start=para.start,
            end=para.end
        ))

    # 整体情感
    overall = aggregate_sentiment(paragraph_sentiments)

    # 情感趋势
    trend = analyze_trend(paragraph_sentiments)

    return SentimentAnalysis(
        overall_sentiment=overall,
        segments=paragraph_sentiments,
        trend=trend,
        positive_ratio=count_positive(paragraph_sentiments) / len(paragraph_sentiments),
        negative_ratio=count_negative(paragraph_sentiments) / len(paragraph_sentiments)
    )
```

## 检查清单

- [ ] 识别准确
- [ ] 强度合理
- [ ] 观点提取
- [ ] 趋势分析
- [ ] 可视化清晰
- [ ] 报告完整

## 红牌警告

- 情感判断错误
- 忽视中性
- 断章取义
- 趋势误判
- 受噪音影响
