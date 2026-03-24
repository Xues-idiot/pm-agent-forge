# 主题提取 (Topic Extraction)

## Overview

主题提取是从播客内容中识别和提取核心主题的技能。用于内容理解、标签生成、搜索索引。

## 何时使用

- 理解播客内容
- 生成内容标签
- 内容分类
- 推荐相关

## 流程

1. **文本预处理**：清洗文本
2. **主题识别**：使用LDA/NMF等识别主题
3. **关键词提取**：提取关键词
4. **层次结构**：构建主题层次
5. **标签生成**：生成可读标签
6. **置信度评估**：评估置信度
7. **可视化**：可视化主题分布

## 模板

### 主题提取模板
```python
TOPIC_CONFIG = {
    "num_topics": 5,
    "min_topic_words": 10,
    "methods": ["lda", "berttopic"],
    "keywords_per_topic": 5
}

def extract_topics(text: str, config: TopicConfig) -> List[Topic]:
    """提取主题"""
    # 文本预处理
    cleaned = preprocess_text(text)

    # BERTopic提取
    model = BERTopic(language="chinese", nr_topics=config.num_topics)
    topics, probs = model.fit_transform(cleaned)

    # 提取主题信息
    return [Topic(
        id=t,
        keywords=model.get_topic(t)[:config.keywords_per_topic],
        confidence=probs[t],
        documents=model.get_topic_docs(t)
    ) for t in topics]
```

## 检查清单

- [ ] 主题准确
- [ ] 关键词相关
- [ ] 覆盖全面
- [ ] 层次清晰
- [ ] 可解释
- [ ] 更新及时

## 红牌警告

- 主题偏离
- 关键词不相关
- 覆盖不全
- 过于宽泛
- 更新滞后
