# 汽车数据采集 (Automobile Data Collection)

## Overview

汽车数据采集是专门用于汽车行业数据采集和分析的技能。支持汽车之家、易车、懂车帝等平台。

## 何时使用

- 车型参数采集
- 价格监控
- 口碑分析
- 竞品对比
- 行业趋势

## 流程

1. **平台选择**：选择汽车平台
2. **车型搜索**：搜索目标车型
3. **数据采集**：采集车型数据
4. **口碑分析**：分析用户口碑
5. **价格监控**：监控价格走势
6. **竞品对比**：对比竞品数据
7. **报告生成**：生成分析报告

## 模板

### 汽车数据采集模板
```python
class AutomobileCollector:
    def __init__(self):
        self.platforms = {
            "autohome": AutohomeSpider(),
            "yiche": YicheSpider(),
            "dongchedi": DongchediSpider()
        }

    async def collect_vehicle(self, vehicle_name: str):
        """采集车型数据"""
        data = {}
        for platform, spider in self.platforms.items():
            try:
                vehicle_data = await spider.get_vehicle(vehicle_name)
                data[platform] = vehicle_data
            except Exception:
                data[platform] = None

        return self.merge_vehicle_data(data)

    async def analyze_reviews(self, vehicle_id: str):
        """分析口碑"""
        reviews = await self.platforms["autohome"].get_reviews(vehicle_id)
        return {
            "total_reviews": len(reviews),
            "overall_score": sum(r.score for r in reviews) / len(reviews),
            "aspect_scores": self.analyze_aspects(reviews),
            "pros": self.extract_pros(reviews),
            "cons": self.extract_cons(reviews),
            "sentiment": self.analyze_sentiment(reviews)
        }

    async def monitor_price(self, vehicle_id: str):
        """监控价格"""
        prices = []
        for _ in range(30):
            price = await self.get_current_price(vehicle_id)
            prices.append({"date": datetime.now(), "price": price})
            await asyncio.sleep(3600)

        return self.analyze_price_trend(prices)
```

## 检查清单

- [ ] 数据完整
- [ ] 参数准确
- [ ] 分析深入
- [ ] 监控及时

## 红牌警告

- 数据缺失
- 参数错误
- 分析偏差
- 反爬封禁
