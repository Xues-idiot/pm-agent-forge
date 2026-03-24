# 洞察挖掘 (Insight Mining)

## Overview

洞察挖掘是从播客内容中提取有价值的见解、观点、数据的技能。

## 何时使用

- 研究学习
- 提炼核心观点
- 收集引用素材
- 发现新角度

## 流程

1. **深度理解**：深度理解内容
2. **洞察识别**：识别潜在洞察
3. **证据提取**：提取支持证据
4. **分类整理**：分类整理洞察
5. **价值评估**：评估洞察价值
6. **引用格式化**：格式化引用
7. **知识入库**：存入知识库

## 模板

### 洞察挖掘模板
```python
@dataclass
class Insight:
    content: str
    type: str  #观点/数据/方法/案例
    source: str
    timestamp: str
    confidence: float
    tags: List[str]

async def mine_insights(transcription: Transcription) -> List[Insight]:
    """挖掘洞察"""
    insights = []

    # 使用LLM提取洞察
    prompt = """
从以下播客内容中提取有价值的洞察：

要求：
1. 每个洞察用一句话概括
2. 标注洞察类型（观点/数据/方法/案例）
3. 标注时间戳
4. 评估置信度(0-1)

格式：
- [观点] 内容 | 类型 | 时间 | 置信度
"""
    result = await llm.generate(prompt + transcription.text)

    # 解析结果
    for line in result.split('\n'):
        if line.strip():
            insights.append(parse_insight(line))

    return sorted(insights, key=lambda x: x.confidence, reverse=True)
```

## 检查清单

- [ ] 洞察有价值
- [ ] 证据充分
- [ ] 分类合理
- [ ] 引用准确
- [ ] 去重干净
- [ ] 知识库同步

## 红牌警告

- 洞察无价值
- 断章取义
- 脱离上下文
- 引用错误
- 重复冗余
