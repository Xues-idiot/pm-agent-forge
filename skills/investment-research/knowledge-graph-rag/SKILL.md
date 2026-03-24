# 知识图谱RAG (Knowledge Graph RAG)

## Overview

知识图谱RAG是构建投研知识图谱并实现智能检索的技能。通过Neo4j等图数据库建立公司、人物、行业、事件间的复杂关系网络。

## 何时使用

- 构建投研知识库
- 分析公司间关联关系
- 发现隐性关联风险
- 产业链关系分析

## 流程

1. **知识抽取**：从研报、公告中抽取实体和关系
2. **图谱设计**：设计图谱schema
3. **数据导入**：导入历史数据
4. **查询构建**：构建投研查询
5. **检索增强**：RAG增强检索
6. **关系推理**：发现隐藏关系
7. **可视化**：图谱可视化

## 模板

### 知识图谱配置模板
```python
# 图谱Schema
ENTITIES = {
    "Company": ["name", "stock_code", "industry", "founded_year"],
    "Person": ["name", "role", "education", "background"],
    "Industry": ["name", "classification", "policy"],
    "Event": ["type", "date", "description", "impact"],
}

RELATIONSHIPS = {
    "Company": {
        "invests": ["Company"],
        "competes": ["Company"],
        "supplies": ["Company"],
        "acquired_by": ["Company"],
        "CEO": ["Person"],
        "belongs_to": ["Industry"],
    }
}

# Neo4j查询示例
QUERY = """
MATCH (c:Company {stock_code: '600519'})
-[:belongs_to]->(i:Industry)
MATCH (c)-[:supplies|competes]->(related:Company)
RETURN c.name, i.name, collect(related.name) as related_companies
"""
```

## 检查清单

- [ ] Schema设计合理
- [ ] 实体关系准确
- [ ] 数据导入完整
- [ ] 查询效率优化
- [ ] RAG增强有效
- [ ] 可视化清晰

## 红牌警告

- Schema设计混乱
- 数据导入遗漏
- 查询性能差
- 关系推断错误
- 信息过时
