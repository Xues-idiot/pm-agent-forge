# 餐饮数据采集 (Dining Data Collection)

## Overview

餐饮数据采集是专门用于餐饮行业数据采集和分析的技能。支持大众点评、美团、饿了么等平台。

## 何时使用

- 餐厅数据采集
- 菜单分析
- 评分监控
- 竞品分析
- 行业趋势

## 流程

1. **平台选择**：选择餐饮平台
2. **餐厅搜索**：搜索目标餐厅
3. **数据采集**：采集餐厅数据
4. **菜单分析**：分析菜单结构
5. **评价分析**：分析用户评价
6. **价格监控**：监控价格变化
7. **报告生成**：生成分析报告

## 模板

### 餐饮数据采集模板
```python
class DiningCollector:
    def __init__(self):
        self.platforms = {
            "dianping": DianpingSpider(),
            "meituan": MeituanSpider(),
            "ele": EleSpider()
        }

    async def collect_restaurant(self, restaurant_name: str, city: str):
        """采集餐厅数据"""
        data = {}
        for platform, spider in self.platforms.items():
            try:
                restaurant = await spider.search(restaurant_name, city)
                data[platform] = restaurant
            except Exception:
                data[platform] = None

        return self.merge_restaurant_data(data)

    async def analyze_reviews(self, restaurant_id: str):
        """分析评价"""
        reviews = await self.platforms["dianping"].get_reviews(restaurant_id)
        return {
            "total": len(reviews),
            "avg_score": sum(r.score for r in reviews) / len(reviews),
            "taste_score": sum(r.taste for r in reviews) / len(reviews),
            "environment_score": sum(r.environment for r in reviews) / len(reviews),
            "service_score": sum(r.service for r in reviews) / len(reviews),
            "keyword_cloud": self.extract_keywords(reviews),
            "recent_trend": self.analyze_score_trend(reviews)
        }

    async def compare_restaurants(self, restaurant_ids: List[str]):
        """对比餐厅"""
        restaurants = []
        for rid in restaurant_ids:
            r = await self.collect_by_id(rid)
            restaurants.append(r)
        return self.rank_restaurants(restaurants)
```

## 检查清单

- [ ] 数据完整
- [ ] 评分准确
- [ ] 分析深入
- [ ] 报告专业

## 红牌警告

- 数据缺失
- 评分错误
- 分析偏差
- 反爬封禁
