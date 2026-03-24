# 新闻资讯垂直浏览器 (News Browser)

## Overview

新闻资讯垂直浏览器是专门用于新闻数据采集和舆情分析的技能。支持各类新闻媒体和资讯平台。

## 何时使用

- 新闻监控
- 舆情分析
- 竞品监控
- 行业动态
- 趋势追踪

## 流程

1. **媒体选择**：选择目标媒体
2. **关键词设置**：设置监控关键词
3. **新闻采集**：采集新闻数据
4. **内容分析**：分析新闻内容
5. **情感判断**：判断情感倾向
6. **趋势分析**：分析传播趋势
7. **报告生成**：生成新闻报告

## 模板

### 新闻数据采集模板
```python
class NewsBrowser:
    def __init__(self):
        self.sources = {
            "wechat": WeChatSpider(),
            "news": NewsSpider(),
            "twitter": TwitterSpider()
        }

    async def search_news(self, keyword: str, sources: List[str] = None):
        """搜索新闻"""
        if not sources:
            sources = list(self.sources.keys())
        results = []
        for source in sources:
            news = await self.sources[source].search(keyword)
            results.extend(news)
        return self.sort_by_date(results)

    async def monitor_topic(self, topic: str, hours: int = 24):
        """监控话题"""
        articles = await self.search_news(topic)
        recent = [a for a in articles if a.is_within_hours(hours)]
        return {
            "total": len(recent),
            "sources": self.count_sources(recent),
            "sentiment": self.analyze_sentiment(recent),
            "传播路径": self.analyze_spread_path(recent)
        }

    async def generate_news_report(self, keyword: str, days: int = 7):
        """生成新闻报告"""
        articles = await self.get_articles_in_range(keyword, days)
        return {
            "summary": self.generate_summary(articles),
            "key_events": self.extract_key_events(articles),
            "media_distribution": self.analyze_distribution(articles),
            "sentiment_trend": self.analyze_sentiment_trend(articles),
            "top_articles": self.get_top_articles(articles, top=10)
        }
```

## 检查清单

- [ ] 来源权威
- [ ] 内容准确
- [ ] 实时性
- [ ] 分析深入
- [ ] 报告专业
- [ ] 覆盖全面

## 红牌警告

- 来源虚假
- 内容错误
- 延迟过高
- 分析偏差
- 遗漏重要
