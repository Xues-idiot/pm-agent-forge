# 旅游垂直浏览器 (Travel Browser)

## Overview

旅游垂直浏览器是专门用于旅游数据采集和规划的技能。支持携程、马蜂窝、Booking等平台。

## 何时使用

- 酒店价格对比
- 机票价格监控
- 旅游攻略采集
- 景点评价分析
- 行程规划辅助

## 流程

1. **平台选择**：选择旅游平台
2. **目的地设置**：设置目的地
3. **数据采集**：采集旅游数据
4. **价格分析**：分析价格走势
5. **攻略整合**：整合旅游攻略
6. **行程规划**：规划旅行行程
7. **成本优化**：优化旅行成本

## 模板

### 旅游数据采集模板
```python
class TravelBrowser:
    def __init__(self):
        self.platforms = {
            "ctrip": CtripSpider(),
            "mafengwo": MafengwoSpider(),
            "booking": BookingSpider()
        }

    async def search_hotels(self, destination: str, dates: DateRange):
        """搜索酒店"""
        hotels = []
        for platform_name, spider in self.platforms.items():
            if "hotel" in spider.capabilities:
                results = await spider.search_hotels(destination, dates)
                hotels.extend(results)
        return self.sort_by_price(hotels)

    async def monitor_flight_price(self, route: str, dates: DateRange):
        """监控机票价格"""
        price_history = []
        for _ in range(7):  # 监控一周
            price = await self.get_flight_price(route, dates)
            price_history.append({"date": datetime.now(), "price": price})
            await asyncio.sleep(3600)  # 每小时检查
        return self.analyze_price_trend(price_history)

    async def generate_travel_plan(self, destination: str, days: int):
        """生成旅行计划"""
        attractions = await self.platforms["mafengwo"].get_attractions(destination)
        hotels = await self.search_hotels(destination, None)
        return self.optimize_itinerary(attractions, hotels, days)
```

## 检查清单

- [ ] 酒店覆盖
- [ ] 机票实时
- [ ] 攻略完整
- [ ] 评价准确
- [ ] 规划合理
- [ ] 成本优化

## 红牌警告

- 数据过期
- 价格错误
- 库存缺失
- 攻略偏差
- 规划不合理
