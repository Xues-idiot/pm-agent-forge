# 摘要生成 (Summary Generation)

## Overview

摘要生成是自动生成播客内容摘要的技能。包括一句话摘要、要点摘要、完整摘要等。

## 何时使用

- 快速了解内容
- 生成节目介绍
- 社交媒体分享
- 时间有限的听众

## 流程

1. **内容理解**：理解完整内容
2. **结构分析**：分析内容结构
3. **关键点识别**：识别关键信息点
4. **摘要生成**：生成多级别摘要
5. **一句话生成**：生成一句话摘要
6. **质量校验**：校验摘要质量
7. **多语言**：支持多语言摘要

## 模板

### 摘要生成模板
```python
SUMMARY_TYPES = {
    "tldr": {"max_length": 20, "style": "一句话"},
    "highlights": {"max_length": 100, "style": "要点列表"},
    "full": {"max_length": 500, "style": "完整摘要"}
}

async def generate_summaries(transcription: Transcription) -> Summaries:
    """生成多级摘要"""
    summaries = {}

    # 一句话摘要
    summaries["tldr"] = await llm.generate(
        f"用一句话概括以下内容的核心：\n{transcription.text[:2000]}"
    )

    # 要点摘要
    summaries["highlights"] = await llm.generate(
        f"提取3-5个要点：\n{transcription.text[:5000]}"
    )

    # 完整摘要
    summaries["full"] = await llm.generate(
        f"生成300字的摘要：\n{transcription.text}"
    )

    return Summaries(**summaries)
```

## 检查清单

- [ ] 摘要准确
- [ ] 覆盖核心
- [ ] 语言流畅
- [ ] 长度合适
- [ ] 多级别
- [ ] 多语言

## 红牌警告

- 摘要偏离
- 遗漏重点
- 语言不通顺
- 长度不当
- 事实错误
