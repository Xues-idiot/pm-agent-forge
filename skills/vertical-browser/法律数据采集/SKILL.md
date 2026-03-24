# 法律数据采集 (Legal Data Collection)

## Overview

法律数据采集是专门用于法律行业数据采集和分析的技能。支持裁判文书、法律法规、律师信息等数据采集。

## 何时使用

- 案例分析
- 律师信息查询
- 法规检索
- 诉讼追踪
- 司法统计

## 流程

1. **数据源选择**：选择法律数据源
2. **案件查询**：查询目标案件
3. **数据采集**：采集案件数据
4. **文书分析**：分析裁判文书
5. **法规关联**：关联相关法规
6. **统计生成**：生成司法统计
7. **报告输出**：输出分析报告

## 模板

### 法律数据采集模板
```python
class LegalCollector:
    def __init__(self):
        self.sources = {
            "court": CourtSpider(),
            "law": LawSpider(),
            "lawyer": LawyerSpider()
        }

    async def search_cases(self, keyword: str, court: str = None):
        """搜索案件"""
        cases = await self.sources["court"].search(keyword, court=court)
        return cases

    async def analyze_case(self, case_id: str):
        """分析案件"""
        case = await self.sources["court"].get_case(case_id)
        return {
            "basic": case.basic_info,
            "parties": case.parties,
            "claims": case.claims,
            "evidence": case.evidence,
            "judgment": case.judgment,
            "related_laws": await self.find_related_laws(case),
            "similar_cases": await self.find_similar(case)
        }

    async def track_lawyer(self, lawyer_name: str):
        """追踪律师"""
        lawyer = await self.sources["lawyer"].get_profile(lawyer_name)
        cases = await self.sources["court"].get_lawyer_cases(lawyer.id)
        return {
            "profile": lawyer,
            "case_count": len(cases),
            "win_rate": self.calculate_win_rate(cases),
            "specialties": self.analyze_specialties(cases),
            "recent_cases": cases[:10]
        }
```

## 检查清单

- [ ] 数据准确
- [ ] 分析客观
- [ ] 法规正确
- [ ] 隐私合规

## 红牌警告

- 数据错误
- 分析偏差
- 法规过时
- 隐私风险
