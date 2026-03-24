# SEO优化 (SEO Optimization)

## Overview

SEO优化是提升搜索引擎排名的技能。包括关键词研究、技术SEO、内容优化、外链建设、数据分析等。

## 何时使用

- 搜索排名
- 流量增长
- 技术优化
- 内容优化
- 竞品分析

## 流程

1. **关键词研究**：研究关键词
2. **技术审计**：审计技术问题
3. **内容优化**：优化内容
4. **外链建设**：建设外链
5. **排名监控**：监控排名
6. **持续优化**：持续优化
7. **报告生成**：生成报告

## 模板

### SEO优化模板
```python
class SEOOptimization:
    async def keyword_research(self, seed: str):
        """关键词研究"""
        keywords = await self.get_keyword_ideas(seed)
        return {
            "primary_keywords": [k for k in keywords if k.volume > 1000],
            "long_tail": [k for k in keywords if k.volume < 500 and k.difficulty < 30],
            "competitor_keywords": await self.get_competitor_keywords(seed),
            "keyword_opportunities": self.find_opportunities(keywords)
        }

    async def technical_audit(self, url: str):
        """技术审计"""
        return {
            "crawlability": await self.check_robots_txt(url),
            "indexability": await self.check_indexation(url),
            "page_speed": await self.check_page_speed(url),
            "mobile_friendly": await self.check_mobile(url),
            "structured_data": await self.check_schema(url),
            "core_web_vitals": await self.check_cwv(url),
            "issues": await self.identify_issues(url),
            "priority_fixes": self.prioritize_fixes()
        }

    async def optimize_content(self, page_id: str, keywords: List[str]):
        """优化内容"""
        return {
            "title": self.optimize_title(keywords),
            "meta_description": self.optimize_meta(keywords),
            "headings": self.optimize_headings(keywords),
            "content": self.optimize_body(keywords),
            "internal_links": self.suggest_internal_links(keywords),
            "images": self.optimize_images(keywords)
        }

    async def track_rankings(self, keywords: List[str]):
        """追踪排名"""
        rankings = {}
        for keyword in keywords:
            rank = await self.get_ranking(keyword)
            rankings[keyword] = {
                "current": rank.position,
                "change": rank.position - rank.previous,
                "search_volume": rank.volume,
                "estimated_traffic": self.estimate_traffic(rank)
            }
        return rankings
```

## 检查清单

- [ ] 关键词精准
- [ ] 技术健康
- [ ] 内容优化
- [ ] 外链质量
- [ ] 排名提升

## 红牌警告

- 关键词堆砌
- 技术问题
- 内容低质
- 外链垃圾
- 排名下降
