# 学术研究垂直浏览器 (Academic Research Browser)

## Overview

学术研究垂直浏览器是专门用于学术论文和研究资料采集的技能。支持Google Scholar、CNKI、PubMed等平台。

## 何时使用

- 论文检索收集
- 文献综述
- 引文分析
- 学术趋势研究
- 科研数据采集

## 流程

1. **数据库选择**：选择学术数据库
2. **检索策略**：制定检索策略
3. **文献采集**：采集学术文献
4. **质量评估**：评估文献质量
5. **引文分析**：分析引文关系
6. **综述生成**：生成文献综述
7. **趋势分析**：分析研究趋势

## 模板

### 学术研究采集模板
```python
class AcademicBrowser:
    def __init__(self):
        self.databases = {
            "scholar": GoogleScholarSpider(),
            "cnki": CNKISpider(),
            "pubmed": PubMedSpider(),
            "arxiv": ArxivSpider()
        }

    async def search_papers(self, query: str, databases: List[str]):
        """搜索学术论文"""
        results = []
        for db in databases:
            papers = await self.databases[db].search(query)
            results.extend(papers)
        return self.deduplicate_and_sort(results)

    async def get_paper_citations(self, paper_id: str, database: str):
        """获取论文引文"""
        citations = await self.databases[database].get_citations(paper_id)
        return self.build_citation_graph(citations)

    async def analyze_research_trend(self, field: str, years: range):
        """分析研究趋势"""
        papers = []
        for year in years:
            year_papers = await self.search_papers(f"year:{year} {field}")
            papers.extend(year_papers)
        return self.analyze_keyword_frequency(papers)

    async def generate_literature_review(self, topic: str):
        """生成文献综述"""
        papers = await self.search_papers(topic, ["scholar", "pubmed"])
        papers = await self.filter_by_quality(papers, min_citations=5)
        return self.write_review(papers)
```

## 检查清单

- [ ] 数据库覆盖
- [ ] 检索全面
- [ ] 引用准确
- [ ] 趋势分析
- [ ] 综述质量
- [ ] 格式规范

## 红牌警告

- 检索不全
- 数据错误
- 引用丢失
- 趋势偏差
- 综述浅薄
