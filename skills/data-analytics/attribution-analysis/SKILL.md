# 归因分析 (Attribution Analysis)

## Overview

归因分析是分析用户转化来源的技能。包括归因模型、渠道贡献、路径分析、ROI分析等。

## 何时使用

- 营销归因
- 渠道评估
- 预算分配
- 用户路径
- ROI分析

## 流程

1. **归因模型**：选择归因模型
2. **数据采集**：采集归因数据
3. **渠道分析**：分析渠道贡献
4. **路径分析**：分析转化路径
5. **ROI分析**：分析渠道ROI
6. **预算优化**：优化预算分配
7. **报告生成**：生成分析报告

## 模板

### 归因分析模板
```python
class AttributionAnalysis:
    def select_model(self, business_type: str):
        """选择归因模型"""
        models = {
            "last_click": "最后一次点击归因",
            "first_click": "首次点击归因",
            "linear": "线性归因",
            "time_decay": "时间衰减归因",
            "position": "位置归因",
            "data_driven": "数据驱动归因"
        }
        return models.get(business_type, "last_click")

    async def analyze_channel_contribution(self, model: str):
        """分析渠道贡献"""
        if model == "last_click":
            sql = """
                SELECT last_channel as channel,
                       COUNT(*) as conversions
                FROM conversions
                GROUP BY last_channel
            """
        elif model == "linear":
            sql = """
                SELECT channel,
                       SUM(1.0 / path_length) as weighted_conversions
                FROM touchpoints
                GROUP BY channel
            """
        # ... other models

        results = await self.execute(sql)
        return self.normalize(results)

    async def analyze_user_journey(self, user_id: str):
        """分析用户路径"""
        touchpoints = await self.get_touchpoints(user_id)
        return {
            "path": [t.channel for t in touchpoints],
            "path_length": len(touchpoints),
            "first_interaction": touchpoints[0].channel if touchpoints else None,
            "last_interaction": touchpoints[-1].channel if touchpoints else None,
            "journey_duration": self.calculate_duration(touchpoints)
        }

    async def optimize_budget(self, total_budget: float):
        """优化预算"""
        channel_data = await self.get_channel_performance()

        # 使用线性规划优化
        allocation = self.linear_optimize(
            channel_data,
            total_budget,
            objective="maximize_conversions"
        )

        return {
            "allocation": allocation,
            "expected_conversions": self.calculate_expected_conversions(allocation),
            "budget_distribution": self.distribute(allocation)
        }
```

## 检查清单

- [ ] 模型选择
- [ ] 数据准确
- [ ] 分析深入
- [ ] 优化合理
- [ ] 报告清晰

## 红牌警告

- 模型错误
- 数据缺失
- 分析偏差
- 优化失当
