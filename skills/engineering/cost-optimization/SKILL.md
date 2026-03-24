# 成本优化 (Cost Optimization)

## Overview

成本优化是分析和优化云成本的技能。包括成本分析、资源优化、架构调整、预算控制等。

## 何时使用

- 成本分析
- 资源优化
- 架构优化
- 预算控制
- 成本报告

## 流程

1. **成本分析**：分析当前成本
2. **资源审计**：审计资源使用
3. **优化方案**：制定优化方案
4. **实施优化**：实施优化措施
5. **效果跟踪**：跟踪优化效果
6. **预算设置**：设置预算告警
7. **持续监控**：持续成本监控

## 模板

### 成本优化模板
```python
class CostOptimization:
    async def analyze_costs(self, period: str = "30d"):
        """分析成本"""
        costs = await self.billing.get_costs(period)
        return {
            "total": costs.total,
            "by_service": costs.group_by("service"),
            "by_region": costs.group_by("region"),
            "by_tag": costs.group_by("tag"),
            "trends": costs.calculate_trends(),
            "anomalies": costs.detect_anomalies()
        }

    async def find_saving_opportunities(self):
        """寻找节省机会"""
        opportunities = []

        # 闲置资源
        idle = await self.find_idle_resources()
        if idle:
            opportunities.append({
                "type": "idle_resources",
                "savings": self.estimate_savings(idle),
                "resources": idle
            })

        # 预留实例
        ris = await self.find_reserved_opportunities()
        if ris:
            opportunities.append({
                "type": "reserved_instances",
                "savings": self.estimate_savings(ris),
                "recommendation": ris
            })

        # 右侧大小
        oversized = await self.find_oversized()
        if oversized:
            opportunities.append({
                "type": "right_sizing",
                "savings": self.estimate_savings(oversized),
                "resources": oversized
            })

        return opportunities

    async def implement_savings(self, opportunity: dict):
        """实施优化"""
        if opportunity["type"] == "idle_resources":
            return await self.stop_resources(opportunity["resources"])
        elif opportunity["type"] == "reserved_instances":
            return await self.purchase_ri(opportunity["recommendation"])
        elif opportunity["type"] == "right_sizing":
            return await self.resize_resources(opportunity["resources"])
```

## 检查清单

- [ ] 成本透明
- [ ] 分析准确
- [ ] 优化有效
- [ ] 预算可控
- [ ] 报告清晰

## 红牌警告

- 成本超支
- 优化过度
- 性能下降
- 报告错误
