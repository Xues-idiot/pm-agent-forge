# 招聘垂直浏览器 (Recruitment Browser)

## Overview

招聘垂直浏览器是专门用于招聘数据采集和分析的技能。支持BOSS直聘、猎聘、拉勾等平台。

## 何时使用

- 职位搜索采集
- 薪资分析
- 竞品招聘分析
- 行业趋势
- 人才地图

## 流程

1. **平台选择**：选择招聘平台
2. **条件设置**：设置搜索条件
3. **数据采集**：采集职位信息
4. **数据清洗**：清洗异常数据
5. **薪资分析**：分析薪资水平
6. **趋势分析**：分析招聘趋势
7. **报告生成**：生成分析报告

## 模板

### 招聘数据采集模板
```python
class RecruitmentBrowser:
    def __init__(self):
        self.platforms = {
            "boss": BossZhipinSpider(),
            "liepin": LiepinSpider(),
            "lagou": LagouSpider()
        }

    async def search_jobs(self, keyword: str, city: str = None):
        """搜索职位"""
        jobs = []
        for platform, spider in self.platforms.items():
            results = await spider.search(keyword, city=city)
            jobs.extend(results)
        return self.deduplicate_jobs(jobs)

    async def analyze_salary(self, jobs: List[Job]):
        """薪资分析"""
        salaries = [j.salary for j in jobs if j.salary]
        return {
            "avg": sum(salaries) / len(salaries),
            "min": min(salaries),
            "max": max(salaries),
            "distribution": self.salary_distribution(salaries),
            "by_experience": self.group_by_experience(jobs),
            "by_company": self.group_by_company(jobs)
        }

    async def analyze_company_recruitment(self, company: str):
        """分析公司招聘情况"""
        jobs = await self.search_jobs(f"公司:{company}")
        return {
            "open_positions": len(jobs),
            "avg_salary": self.calculate_avg_salary(jobs),
            "hot_roles": self.find_hot_roles(jobs),
            "growth_trend": await self.compare_with_history(company)
        }
```

## 检查清单

- [ ] 平台覆盖
- [ ] 数据完整
- [ ] 分析准确
- [ ] 报告专业

## 红牌警告

- 数据缺失
- 薪资错误
- 分析偏差
- 反爬封禁
