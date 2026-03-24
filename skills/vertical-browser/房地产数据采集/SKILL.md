# 房地产数据采集 (Real Estate Data Collection)

## Overview

房地产数据采集是专门用于房地产行业全链路数据采集的技能。支持新房、二手房、租房、开发商等多维度数据。

## 何时使用

- 新盘监控
- 二手房采集
- 租房数据
- 开发商分析
- 区域分析

## 流程

1. **平台选择**：选择房地产平台
2. **数据采集**：采集房源数据
3. **数据清洗**：清洗无效数据
4. **价格分析**：分析价格走势
5. **区域分析**：分析区域热度
6. **开发商分析**：分析开发商资质
7. **报告生成**：生成分析报告

## 模板

### 房地产数据采集模板
```python
class RealEstateCollector:
    def __init__(self):
        self.platforms = {
            "lianjia": LianjiaSpider(),
            "beike": BeikeSpider(),
            "anjuke": AnjukeSpider(),
            "fang": FangSpider()
        }

    async def collect_new_properties(self, city: str):
        """采集新盘数据"""
        properties = []
        for platform, spider in self.platforms.items():
            try:
                new_props = await spider.get_new_properties(city)
                properties.extend(new_props)
            except Exception:
                continue
        return self.deduplicate_properties(properties)

    async def analyze_price_trend(self, district: str, period: str = "1y"):
        """分析价格趋势"""
        history = await self.get_price_history(district, period)
        return {
            "current_price": history[-1].price,
            "price_change": self.calculate_change(history),
            "avg_price": sum(h.price for h in history) / len(history),
            "trend": self.analyze_trend(history),
            "forecast": self.predict_future(history)
        }

    async def analyze developer(self, developer_name: str):
        """分析开发商"""
        info = await self.platforms["beike"].get_developer(developer_name)
        projects = await self.platforms["beike"].get_developer_projects(developer_name)
        return {
            "basic": info,
            "project_count": len(projects),
            "avg_price": sum(p.price for p in projects) / len(projects),
            "quality_score": self.calculate_quality_score(projects),
            "reputation": self.analyze_reputation(projects)
        }
```

## 检查清单

- [ ] 数据完整
- [ ] 价格准确
- [ ] 分析深入
- [ ] 监控及时

## 红牌警告

- 数据缺失
- 价格错误
- 分析偏差
- 反爬封禁
