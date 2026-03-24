# 物流数据采集 (Logistics Data Collection)

## Overview

物流数据采集是专门用于物流行业数据采集和分析的技能。支持快递、货运、仓储等多维度数据。

## 何时使用

- 快递追踪
- 运费比较
- 物流监控
- 仓储分析
- 供应链优化

## 流程

1. **数据源选择**：选择物流数据源
2. **运单追踪**：追踪运单状态
3. **运费查询**：查询运费价格
4. **时效分析**：分析物流时效
5. **异常监控**：监控物流异常
6. **成本分析**：分析物流成本
7. **报告生成**：生成分析报告

## 模板

### 物流数据采集模板
```python
class LogisticsCollector:
    def __init__(self):
        self.express = {
            "sf": SFExpressAPI(),
            "jd": JDLogisticsAPI(),
            "ems": EMSAPI()
        }
        self.freight = FreightPlatforms()

    async def track_package(self, tracking_number: str, carrier: str):
        """追踪包裹"""
        api = self.express.get(carrier)
        return await api.track(tracking_number)

    async def compare_freight(self, from_city: str, to_city: str, weight: float):
        """比较运费"""
        rates = []
        for carrier, api in self.express.items():
            try:
                rate = await api.get_rate(from_city, to_city, weight)
                rates.append({"carrier": carrier, "rate": rate})
            except Exception:
                continue
        return sorted(rates, key=lambda x: x["rate"])

    async def analyze_delivery_performance(self, carrier: str):
        """分析配送绩效"""
        data = await self.get_delivery_data(carrier)
        return {
            "on_time_rate": sum(d.on_time for d in data) / len(data),
            "avg_delivery_time": sum(d.delivery_time for d in data) / len(data),
            "damage_rate": sum(d.damaged for d in data) / len(data),
            "complaint_rate": sum(d.complaints for d in data) / len(data),
            "trend": self.analyze_trend(data)
        }
```

## 检查清单

- [ ] 数据准确
- [ ] 追踪及时
- [ ] 分析客观
- [ ] 报告清晰

## 红牌警告

- 数据延迟
- 追踪失败
- 分析偏差
- 成本高估
