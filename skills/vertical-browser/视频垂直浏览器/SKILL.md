# 视频垂直浏览器 (Video Browser)

## Overview

视频垂直浏览器是专门用于视频内容采集和处理的技能。支持B站、YouTube、爱奇艺等平台。

## 何时使用

- 视频数据采集
- 弹幕/评论分析
- 视频内容提取
- 创作者数据监控
- 热门视频追踪

## 流程

1. **平台选择**：选择视频平台
2. **内容定位**：定位目标内容
3. **数据采集**：采集视频数据
4. **内容处理**：处理视频内容
5. **数据分析**：分析视频数据
6. **监控设置**：设置数据监控
7. **报告生成**：生成分析报告

## 模板

### 视频数据采集模板
```python
class VideoBrowser:
    def __init__(self):
        self.platforms = {
            "bilibili": BilibiliSpider(),
            "youtube": YoutubeSpider(),
            "iqiyi": IqiyiSpider()
        }

    async def get_video_info(self, url: str):
        """获取视频信息"""
        platform = self.detect_platform(url)
        video_info = await self.platforms[platform].get_info(url)
        return self.normalize_video_info(video_info)

    async def get_comments(self, url: str, limit: int = 100):
        """获取视频评论"""
        platform = self.detect_platform(url)
        comments = await self.platforms[platform].get_comments(url, limit)
        return self.analyze_sentiment(comments)

    async def monitor_creator(self, creator_id: str):
        """监控创作者数据"""
        data = await self.platforms["bilibili"].get_creator_stats(creator_id)
        return {
            "followers": data["follower_count"],
            "views": data["total_views"],
            "trend": self.calculate_trend(data["history"])
        }

    async def track_trending(self, platform: str, category: str):
        """追踪热门视频"""
        trending = await self.platforms[platform].get_trending(category)
        return self.analyze_trending_patterns(trending)
```

## 检查清单

- [ ] 平台覆盖
- [ ] 数据完整
- [ ] 内容准确
- [ ] 分析深入
- [ ] 监控有效
- [ ] 报告清晰

## 红牌警告

- 数据缺失
- 解析失败
- 反爬封禁
- 分析偏差
- 监控延迟
