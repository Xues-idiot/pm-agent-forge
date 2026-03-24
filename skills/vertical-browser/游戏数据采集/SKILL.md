# 游戏数据采集 (Gaming Data Collection)

## Overview

游戏数据采集是专门用于游戏行业数据采集和分析的技能。支持TapTap、Steam、App Store等平台。

## 何时使用

- 游戏数据采集
- 评分监控
- 竞品分析
- 版本追踪
- 玩家反馈

## 流程

1. **平台选择**：选择游戏平台
2. **游戏搜索**：搜索目标游戏
3. **数据采集**：采集游戏数据
4. **评价分析**：分析玩家评价
5. **版本追踪**：追踪版本更新
6. **竞品对比**：对比同类游戏
7. **报告生成**：生成分析报告

## 模板

### 游戏数据采集模板
```python
class GamingCollector:
    def __init__(self):
        self.platforms = {
            "taptap": TapTapSpider(),
            "steam": SteamSpider(),
            "appstore": AppStoreSpider()
        }

    async def collect_game(self, game_name: str):
        """采集游戏数据"""
        data = {}
        for platform, spider in self.platforms.items():
            try:
                game = await spider.get_game(game_name)
                data[platform] = game
            except Exception:
                data[platform] = None

        return self.merge_game_data(data)

    async def analyze_reviews(self, game_id: str, platform: str):
        """分析评价"""
        reviews = await self.platforms[platform].get_reviews(game_id)
        return {
            "total": len(reviews),
            "avg_score": sum(r.score for r in reviews) / len(reviews),
            "score_distribution": self.score_distribution(reviews),
            "keywords": self.extract_keywords(reviews),
            "positive_aspects": self.extract_positives(reviews),
            "negative_aspects": self.extract_negatives(reviews),
            "recent_trend": self.analyze_score_trend(reviews)
        }

    async def track_version(self, game_id: str, platform: str):
        """追踪版本更新"""
        versions = await self.platforms[platform].get_versions(game_id)
        return {
            "current_version": versions[0] if versions else None,
            "update_frequency": self.calculate_update_freq(versions),
            "recent_updates": versions[:5],
            "update_sentiment": self.analyze_update_reviews(versions)
        }
```

## 检查清单

- [ ] 数据完整
- [ ] 评分准确
- [ ] 追踪及时
- [ ] 分析深入

## 红牌警告

- 数据缺失
- 评分错误
- 追踪延迟
- 反爬封禁
