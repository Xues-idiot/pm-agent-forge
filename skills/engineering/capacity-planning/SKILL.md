# 容量规划 (Capacity Planning)

## Overview

容量规划是进行系统容量预测和资源规划的技能。包括容量评估、需求预测、资源规划、成本优化等。

## 何时使用

- 容量评估
- 扩缩容规划
- 成本优化
- 性能测试
- 年度规划

## 流程

1. **现状分析**：分析当前容量
2. **需求预测**：预测未来需求
3. **容量建模**：建立容量模型
4. **差距分析**：分析容量差距
5. **方案设计**：设计扩容方案
6. **成本评估**：评估成本影响
7. **实施规划**：规划实施步骤

## 模板

### 容量规划模板
```python
class CapacityPlanning:
    async def assess_capacity(self, service: Service):
        """评估容量"""
        metrics = await self.collect_metrics(service)
        return {
            "current_utilization": {
                "cpu": metrics.avg_cpu,
                "memory": metrics.avg_memory,
                "disk": metrics.avg_disk,
                "network": metrics.avg_bandwidth
            },
            "bottlenecks": self.identify_bottlenecks(metrics),
            "headroom": self.calculate_headroom(metrics),
            "limits": {
                "max_concurrent": metrics.max_concurrent,
                "max_throughput": metrics.max_throughput
            }
        }

    async def forecast_demand(self, service: Service, months: int):
        """预测需求"""
        history = await self.get_demand_history(service, months=12)
        trend = self.fit_trend(history)
        seasonality = self.extract_seasonality(history)
        return {
            "monthly_forecast": self.forecast(trend, seasonality, months),
            "peak_prediction": self.predict_peak(history),
            "confidence_interval": self.confidence_interval(trend)
        }

    async def plan_expansion(self, service: Service, target_capacity: int):
        """规划扩容"""
        current = await self.assess_capacity(service)
        gap = target_capacity - current.limits.max_concurrent
        return {
            "current_capacity": current.limits.max_concurrent,
            "target_capacity": target_capacity,
            "gap": gap,
            "options": [
                {"type": "vertical", "cost": self.estimate_vs_cost(gap)},
                {"type": "horizontal", "cost": self.estimate_hs_cost(gap)}
            ],
            "recommendation": self.recommend(gap)
        }
```

## 检查清单

- [ ] 数据完整
- [ ] 模型准确
- [ ] 预测合理
- [ ] 成本可控
- [ ] 实施可行

## 红牌警告

- 数据缺失
- 模型偏差
- 预测失准
- 成本超支
