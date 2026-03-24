# 内容搜索 (Content Search)

## Overview

内容搜索是在播客内容库中进行语义搜索的技能。支持全文搜索、语义搜索、时间范围搜索等。

## 何时使用

- 内容检索
- 知识问答
- 相关片段
- 历史回顾
- 内容挖掘

## 流程

1. **查询理解**：理解搜索意图
2. **检索策略**：制定检索策略
3. **语义搜索**：执行语义搜索
4. **结果排序**：排序搜索结果
5. **上下文提取**：提取相关上下文
6. **结果优化**：优化展示效果

## 模板

### 内容搜索模板
```python
class PodcastSearch:
    def __init__(self):
        self.vector_store = VectorStore()
        self.keyword_index = KeywordIndex()
        self.reranker = CrossEncoderReranker()

    async def search(self, query: str, filters: SearchFilters = None):
        """搜索播客内容"""
        # 1. 理解查询
        query_embedding = await self.get_embedding(query)

        # 2. 向量搜索
        vector_results = await self.vector_store.search(
            query_embedding,
            top_k=50
        )

        # 3. 关键词搜索
        if filters and filters.keyword:
            keyword_results = await self.keyword_index.search(
                filters.keyword,
                filters
            )
            results = self.merge_results(vector_results, keyword_results)
        else:
            results = vector_results

        # 4. 重排序
        reranked = await self.reranker.rerank(query, results)

        # 5. 提取上下文
        for item in reranked:
            item.context = await self.extract_context(item, window=60)

        return SearchResults(
            query=query,
            total=len(reranked),
            results=reranked[:20]
        )

    async def extract_context(self, result: SearchResult, window: int):
        """提取上下文"""
        start = max(0, result.timestamp - window)
        end = result.timestamp + window
        return await self.get_transcript_window(
            result.episode_id,
            start,
            end
        )
```

## 检查清单

- [ ] 检索准确
- [ ] 排序合理
- [ ] 上下文完整
- [ ] 响应快速

## 红牌警告

- 检索遗漏
- 排序不合理
- 上下文截断
- 响应超时
