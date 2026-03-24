# 房产垂直浏览器 (Real Estate Browser)

## Overview

房产垂直浏览器是专门用于房产数据采集和分析的技能。支持链家、贝壳、安居客等平台。

## 何时使用

- 房价走势分析
- 区域房产对比
- 新盘监控
- 租房信息采集
- 房产数据报告

## 流程

1. **平台选择**：选择目标房产平台
2. **搜索配置**：配置搜索条件
3. **数据采集**：采集房源信息
4. **数据清洗**：清洗无效数据
5. **价格分析**：分析价格走势
6. **报告生成**：生成分析报告
7. **监控设置**：设置价格监控

## 模板

### 房产数据采集模板
```python
class RealEstateBrowser:
    def __init__(self):
        self.platforms = {
            "lianjia": LianjiaSpider(),
            "beike": BeikeSpider(),
            "anjuke": AnjukeSpider()
        }

    async def search_properties(self, criteria: SearchCriteria):
        """搜索房源"""
        results = []
        for platform_name, spider in self.platforms.items():
            items = await spider.search(criteria)
            results.extend(items)
        return self.deduplicate(results)

    async def analyze_price_trend(self, district: str):
        """分析价格趋势"""
        history = await self.get_price_history(district)
        return {
            "current": self.calculate_avg(history[-30:]),
            "trend": self.calculate_trend(history),
            "forecast": self.predict_future(history)
        }

    async def monitor_new_listings(self, districts: List[str]):
        """监控新上房源"""
        new_listings = []
        for district in districts:
            listings = await self.platforms["beike"].get_new_listings(district)
            new_listings.extend(listings)
        return new_listings
```

## 检查清单

- [ ] 平台覆盖
- [ ] 数据完整
- [ ] 价格准确
- [ ] 趋势分析
- [ ] 监控有效
- [ ] 报告专业

## 红牌警告

- 数据缺失
- 价格错误
- 趋势偏差
- 监控失效
- 反爬封禁
