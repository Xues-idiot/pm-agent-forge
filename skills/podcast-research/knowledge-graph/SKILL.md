# 知识图谱构建 (Knowledge Graph Construction)

## Overview

知识图谱构建是从播客内容构建知识网络的技能。

## 何时使用

- 知识管理
- 关系发现
- 内容索引
- 智能问答

## 流程

1. **实体识别**：识别实体
2. **关系抽取**：抽取关系
3. **知识融合**：融合知识
4. **图谱构建**：构建图谱
5. **质量校验**：校验图谱
6. **存储查询**：存储和查询
7. **应用输出**：应用到场景

## 模板

### 知识图谱配置
```python
async def build_knowledge_graph(transcription: Transcription) -> KnowledgeGraph:
    """构建知识图谱"""
    # 实体识别
    entities = await ner_model.extract(transcription.text)

    # 关系抽取
    relationships = []
    for entity1 in entities:
        for entity2 in entities:
            if entity1 != entity2:
                relation = find_relation(entity1, entity2, transcription.text)
                if relation:
                    relationships.append(Relation(
                        source=entity1,
                        target=entity2,
                        type=relation.type,
                        confidence=relation.confidence
                    ))

    # 构建图谱
    graph = KnowledgeGraph()
    for entity in entities:
        graph.add_node(entity)
    for rel in relationships:
        graph.add_edge(rel.source, rel.target, relation=rel.type)

    return graph

# 示例查询
def query_knowledge_graph(graph: KnowledgeGraph, entity: str) -> List[Path]:
    """查询图谱"""
    return graph.find_connections(entity, depth=2)
```

## 检查清单

- [ ] 实体识别
- [ ] 关系准确
- [ ] 去重有效
- [ ] 图谱一致
- [ ] 查询可用
- [ ] 更新及时

## 红牌警告

- 实体遗漏
- 关系错误
- 图谱不一致
- 性能问题
- 存储溢出
