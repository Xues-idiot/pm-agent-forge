# 向量数据库集成 (Vector Database Integration)

## Overview

向量数据库集成是使用ChromaDB等存储和检索向量嵌入的技能。用于RAG系统的文档存储和相似性检索。

## 何时使用

- 研报向量存储
- 相似文档检索
- RAG增强
- 语义搜索

## 流程

1. **向量库选择**：选择向量数据库
2. **嵌入模型**：选择嵌入模型
3. **数据处理**：处理和分割文档
4. **向量存储**：存储向量
5. **检索优化**：优化检索
6. **更新管理**：管理向量更新
7. **监控**：监控检索效果

## 模板

### ChromaDB模板
```python
import chromadb
from chromadb.config import Settings
from sentence_transformers import SentenceTransformer

# 初始化客户端
client = chromadb.Client(Settings(
    persist_directory="./vector_store",
    anonymized_telemetry=False
))

# 嵌入模型
embedding_model = SentenceTransformer('all-MiniLM-L6-v2')

# 创建集合
collection = client.create_collection(
    name="research_reports",
    metadata={"description": "投研报告向量库"}
)

# 添加文档
def add_report(report_id: str, content: str, metadata: dict):
    embedding = embedding_model.encode(content)
    collection.add(
        ids=[report_id],
        embeddings=[embedding.tolist()],
        documents=[content],
        metadatas=[metadata]
    )

# 检索
def search_reports(query: str, top_k: int = 5):
    query_embedding = embedding_model.encode(query)
    results = collection.query(
        query_embeddings=[query_embedding.tolist()],
        n_results=top_k
    )
    return results
```

## 检查清单

- [ ] 嵌入模型选择合适
- [ ] 分块策略合理
- [ ] 检索效果验证
- [ ] 更新机制完善
- [ ] 性能可接受
- [ ] 备份恢复

## 红牌警告

- 嵌入质量差
- 分块不合理
- 检索不准确
- 存储膨胀
- 检索延迟高
