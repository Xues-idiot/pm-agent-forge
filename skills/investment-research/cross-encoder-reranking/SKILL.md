# Cross-Encoder重排序 (Cross-Encoder Re-ranking)

## Overview

Cross-Encoder重排序是使用机器学习模型对检索结果重新排序的技能。优先返回金融相关性最高的文档，而非通用相关度最高的。

## 何时使用

- RAG检索结果优化
- 提升信息相关度
- 过滤噪音信息
- 增强研报质量

## 流程

1. **初检**：使用稀疏检索（如BM25）获取候选文档
2. **特征提取**：使用Cross-Encoder提取相关性特征
3. **重排序**：基于分数重排序
4. **阈值过滤**：过滤低相关性文档
5. **结果返回**：返回重排后结果
6. **效果评估**：评估重排效果
7. **模型优化**：根据反馈优化模型

## 模板

### Cross-Encoder配置模板
```python
from sentence_transformers import CrossEncoder

# 模型选择
cross_encoder = CrossEncoder('cross-encoder/ms-marco-MiniLM-L-6-v2')

# 重排流程
def rerank_documents(query: str, documents: list, top_k: int = 5):
    # 创建query-document对
    pairs = [(query, doc) for doc in documents]

    # 获取相关性分数
    scores = cross_encoder.predict(pairs)

    # 按分数排序
    ranked_indices = scores.argsort()[::-1][:top_k]

    # 返回排序后结果
    return [documents[i] for i in ranked_indices]

# 金融领域微调
finance_model = CrossEncoder('cross-encoder/ms-marco-MiniLM-L-6-v2')
finance_model.fit(train_df, epochs=3)
```

## 检查清单

- [ ] 模型选择合适
- [ ] 重排效果验证
- [ ] 阈值设置合理
- [ ] 延迟可接受
- [ ] 效果优于初检
- [ ] 持续优化机制

## 红牌警告

- 重排反而降低相关度
- 模型不适用金融领域
- 延迟过高影响体验
- 阈值过严丢失重要信息
- 过度依赖重排忽视初检
