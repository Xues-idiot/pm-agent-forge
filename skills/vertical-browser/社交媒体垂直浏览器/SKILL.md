# 社交媒体垂直浏览器 (Social Media Browser)

## Overview

社交媒体垂直浏览器是专门用于社交媒体数据采集和舆情分析的技能。支持微博、抖音、小红书等平台。

## 何时使用

- 舆情监控
- KOL分析
- 热点追踪
- 用户画像
- 竞品监控

## 流程

1. **平台选择**：选择社交平台
2. **关键词设置**：设置监控关键词
3. **数据采集**：采集社交数据
4. **情感分析**：分析情感倾向
5. **影响力分析**：分析KOL影响力
6. **趋势分析**：分析热点趋势
7. **报告生成**：生成舆情报告

## 模板

### 社交媒体数据采集模板
```python
class SocialMediaBrowser:
    def __init__(self):
        self.platforms = {
            "weibo": WeiboSpider(),
            "douyin": DouyinSpider(),
            "xiaohongshu": XHSpider()
        }

    async def monitor_keywords(self, keywords: List[str]):
        """监控关键词"""
        posts = []
        for platform_name, spider in self.platforms.items():
            for keyword in keywords:
                results = await spider.search(keyword)
                posts.extend(results)
        return self.deduplicate(posts)

    async def analyze_sentiment(self, posts: List[Post]):
        """情感分析"""
        for post in posts:
            sentiment = await self.sentiment_model.predict(post.content)
            post.sentiment = sentiment
        return self.aggregate_sentiment(posts)

    async def identify_kol(self, platform: str, niche: str):
        """识别KOL"""
        creators = await self.platforms[platform].top_creators(niche)
        return await self.enrich_kol_data(creators)

    async def track_trending(self, platform: str, hours: int = 24):
        """追踪热点"""
        posts = await self.platforms[platform].recent_posts(hours)
        return self.extract_trending_topics(posts)

    async def generate_social_report(self, keyword: str):
        """生成社交媒体报告"""
        posts = await self.monitor_keywords([keyword])
        sentiment = await self.analyze_sentiment(posts)
        trending = await self.track_trending(keyword)
        return {
            "volume": len(posts),
            "sentiment": sentiment,
            "trending": trending,
            "top_posts": self.get_top_posts(posts)
        }
```

## 检查清单

- [ ] 平台覆盖
- [ ] 数据完整
- [ ] 分析准确
- [ ] 监控及时
- [ ] 报告专业
- [ ] 隐私合规

## 红牌警告

- 数据缺失
- 分析偏差
- 隐私风险
- 封号风险
- 延迟过高
