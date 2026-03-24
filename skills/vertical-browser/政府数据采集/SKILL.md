# 政府数据采集 (Government Data Collection)

## Overview

政府数据采集是专门用于政府公开数据采集和分析的技能。支持政策文件、采购公告、统计数据等多维度数据。

## 何时使用

- 政策收集
- 采购监控
- 统计数据
- 招标追踪
- 法规更新

## 流程

1. **数据源选择**：选择政府数据源
2. **数据采集**：采集政府数据
3. **政策解析**：解析政策文件
4. **采购分析**：分析采购公告
5. **统计整理**：整理统计数据
6. **告警设置**：设置更新告警
7. **报告生成**：生成分析报告

## 模板

### 政府数据采集模板
```python
class GovernmentCollector:
    def __init__(self):
        self.sources = {
            "gov": GovSpider(),
            "procurement": ProcurementSpider(),
            "stats": StatsSpider()
        }

    async def search_policies(self, keyword: str, department: str = None):
        """搜索政策"""
        policies = await self.sources["gov"].search(keyword, department)
        return policies

    async def analyze_policy(self, policy_id: str):
        """分析政策"""
        policy = await self.sources["gov"].get_policy(policy_id)
        return {
            "title": policy.title,
            "department": policy.department,
            "date": policy.publish_date,
            "key_points": self.extract_key_points(policy.content),
            "impact": self.analyze_impact(policy),
            "related_policies": await self.find_related(policy)
        }

    async def track_procurement(self, keyword: str, budget_range: tuple = None):
        """追踪采购"""
        procurements = await self.sources["procurement"].search(
            keyword, budget_range
        )
        return {
            "total": len(procurements),
            "total_budget": sum(p.budget for p in procurements),
            "recent": procurements[:10],
            "trends": self.analyze_trends(procurements)
        }
```

## 检查清单

- [ ] 数据权威
- [ ] 更新及时
- [ ] 解析准确
- [ ] 报告专业

## 红牌警告

- 数据过时
- 解析错误
- 遗漏重要
- 报告混乱
