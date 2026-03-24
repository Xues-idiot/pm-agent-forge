# 教育数据采集 (Education Data Collection)

## Overview

教育数据采集是专门用于教育行业数据采集和分析的技能。支持K12、留学、职业技能等多领域数据。

## 何时使用

- 课程数据采集
- 学校信息查询
- 培训评价分析
- 留学数据
- 教育趋势

## 流程

1. **平台选择**：选择教育平台
2. **数据采集**：采集教育数据
3. **评价分析**：分析用户评价
4. **价格分析**：分析课程价格
5. **质量评估**：评估教育质量
6. **趋势分析**：分析教育趋势
7. **报告生成**：生成分析报告

## 模板

### 教育数据采集模板
```python
class EducationCollector:
    def __init__(self):
        self.platforms = {
            "xek": XEKSpider(),      # K12教育
            "zaixian": ZaixianSpider(), # 职业技能
            "liuxue": LiuxueSpider()   # 留学
        }

    async def collect_courses(self, keyword: str, category: str):
        """采集课程数据"""
        courses = []
        platform = self.get_platform(category)
        results = await platform.search(keyword)
        courses.extend(results)
        return courses

    async def analyze_course(self, course_id: str, platform: str):
        """分析课程"""
        course = await self.platforms[platform].get_course(course_id)
        reviews = await self.platforms[platform].get_reviews(course_id)
        return {
            "basic": course,
            "reviews": reviews,
            "avg_score": sum(r.score for r in reviews) / len(reviews),
            "pros": self.extract_pros(reviews),
            "cons": self.extract_cons(reviews),
            "value_score": self.calculate_value_score(course, reviews)
        }

    async def compare_schools(self, school_names: List[str]):
        """对比学校"""
        schools = []
        for name in school_names:
            school = await self.platforms["xek"].get_school(name)
            schools.append(school)
        return self.rank_schools(schools)
```

## 检查清单

- [ ] 数据完整
- [ ] 评价客观
- [ ] 分析深入
- [ ] 隐私合规

## 红牌警告

- 数据缺失
- 评价失真
- 分析偏差
- 隐私风险
