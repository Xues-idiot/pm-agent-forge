# 问答提取 (Q&A Extraction)

## Overview

问答提取是从播客内容中识别和提取问答内容的技能。

## 何时使用

- 提取常见问题
- 制作FAQ
- 索引检索
- 学习问答

## 流程

1. **问题识别**：识别问答模式
2. **答案提取**：提取对应答案
3. **结构化**：结构化输出
4. **质量校验**：校验Q&A质量
5. **格式转换**：转换为目标格式
6. **存储索引**：存储建立索引
7. **应用输出**：应用到其他场景

## 模板

### 问答提取配置
```python
Q&A_PATTERNS = [
    (r"问：(.+)", r"答：(.+)"),
    (r"Q：(.*)", r"A：(.*)"),
    (r"(\d+)、(.+)？(.+)"),
]

async def extract_qa(transcription: Transcription) -> List[QA]:
    """提取问答"""
    qa_pairs = []

    for segment in transcription.segments:
        text = segment.text

        # 模式匹配
        for q_pattern, a_pattern in Q&A_PATTERNS:
            q_match = re.search(q_pattern, text)
            if q_match:
                question = q_match.group(1)

                # 查找对应答案
                answer = find_answer(text, q_match.end())
                if answer:
                    qa_pairs.append(QA(
                        question=question,
                        answer=answer,
                        timestamp=f"{segment.start}-{segment.end}",
                        confidence=0.9
                    ))

    # LLM补充识别
    llm_qa = await llm.extract_qa(transcription.text)
    qa_pairs.extend(llm_qa)

    return deduplicate_qa(qa_pairs)
```

## 检查清单

- [ ] 识别准确
- [ ] 匹配正确
- [ ] 答案相关
- [ ] 去重有效
- [ ] 格式规范
- [ ] 索引可用

## 红牌警告

- 识别错误
- 答案不相关
- 重复冗余
- 格式混乱
- 索引失败
