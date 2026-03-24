# VADER情感分析 (VADER Sentiment Analysis)

## Overview

VADER情感分析是使用VADER模型分析市场情绪的技能。特别适用于社交媒体和新闻的情感量化。

## 何时使用

- 新闻情感量化
- 社交媒体情绪
- 舆情监控
- 市场情绪判断

## 流程

1. **文本收集**：收集新闻/社交文本
2. **预处理**：清洗文本
3. **情感分析**：VADER情感打分
4. **聚合分析**：聚合时间序列
5. **异常检测**：检测情绪异常
6. **信号生成**：生成交易信号
7. **效果验证**：验证预测效果

## 模板

### VADER情感分析模板
```python
from vaderSentiment.vaderSentiment import SentimentIntensityAnalyzer

analyzer = SentimentIntensityAnalyzer()

def analyze_sentiment(text: str) -> dict:
    scores = analyzer.polarity_scores(text)
    return {
        'compound': scores['compound'],  # 综合得分 -1到1
        'pos': scores['pos'],  # 正面比例
        'neg': scores['neg'],  # 负面比例
        'neu': scores['neu'],  # 中性比例
        'sentiment': 'positive' if scores['compound'] > 0.05
                    else 'negative' if scores['compound'] < -0.05
                    else 'neutral'
    }

# 时间序列聚合
def aggregate_sentiment(dates: list, texts: list) -> pd.DataFrame:
    daily_sentiment = []
    for date, text in zip(dates, texts):
        score = analyze_sentiment(text)['compound']
        daily_sentiment.append({'date': date, 'sentiment': score})
    return pd.DataFrame(daily_sentiment).groupby('date')['sentiment'].mean()
```

## 检查清单

- [ ] 数据来源可靠
- [ ] 文本预处理正确
- [ ] 情感判断准确
- [ ] 聚合方法合理
- [ ] 信号生成有效
- [ ] 效果验证可信

## 红牌警告

- 文本来源噪音大
- 情感判断错误
- 忽视时效性
- 过度依赖单一来源
- 信号过于频繁
