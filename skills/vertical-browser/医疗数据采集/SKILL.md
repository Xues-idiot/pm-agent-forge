# 医疗数据采集 (Medical Data Collection)

## Overview

医疗数据采集是专门用于医疗行业数据采集和分析的技能。支持挂号网、好大夫、丁香园等平台。

## 何时使用

- 医院数据采集
- 医生信息查询
- 科室分析
- 评价分析
- 预约难度分析

## 流程

1. **平台选择**：选择医疗平台
2. **医院搜索**：搜索目标医院
3. **医生查询**：查询医生信息
4. **评价分析**：分析患者评价
5. **预约分析**：分析预约难度
6. **数据汇总**：汇总多平台数据
7. **报告生成**：生成分析报告

## 模板

### 医疗数据采集模板
```python
class MedicalCollector:
    def __init__(self):
        self.platforms = {
            "guahao": GuahaoSpider(),
            "haodf": HaodfSpider(),
            "dxy": DXYSpider()
        }

    async def collect_doctor(self, doctor_name: str, hospital: str):
        """采集医生数据"""
        data = {}
        for platform, spider in self.platforms.items():
            try:
                doctor = await spider.get_doctor(doctor_name, hospital)
                data[platform] = doctor
            except Exception:
                data[platform] = None

        return self.merge_doctor_data(data)

    async def analyze_reviews(self, doctor_id: str):
        """分析评价"""
        reviews = await self.platforms["haodf"].get_reviews(doctor_id)
        return {
            "total": len(reviews),
            "positive_rate": sum(1 for r in reviews if r.rating >= 4) / len(reviews),
            "avg_rating": sum(r.rating for r in reviews) / len(reviews),
            "keywords": self.extract_keywords(reviews),
            "treatment_types": self.analyze_treatments(reviews),
            "sentiment": self.analyze_sentiment(reviews)
        }

    async def compare_hospitals(self, hospital_names: List[str], city: str):
        """对比医院"""
        hospitals = []
        for name in hospital_names:
            h = await self.platforms["guahao"].search_hospital(name, city)
            hospitals.append(h)
        return self.rank_hospitals(hospitals)
```

## 检查清单

- [ ] 数据准确
- [ ] 信息完整
- [ ] 分析客观
- [ ] 隐私合规

## 红牌警告

- 数据错误
- 信息过时
- 分析偏差
- 隐私风险
