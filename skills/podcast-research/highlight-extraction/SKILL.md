# 高光时刻提取 (Highlight Extraction)

## Overview

高光时刻提取是识别播客中最精彩、最有价值片段的技能。

## 何时使用

- 制作精彩集锦
- 内容预览
- 社交分享
- 时间戳导航

## 流程

1. **多维评分**：多维度评分片段
2. **兴奋度检测**：检测语音兴奋度
3. **内容重要性**：评估内容重要性
4. **社交互动**：分析互动数据
5. **综合排序**：综合排序高光
6. **片段剪辑**：剪辑高光片段
7. **描述生成**：生成高光描述

## 模板

### 高光提取配置
```python
HIGHLIGHT_CONFIG = {
    "min_score": 0.7,
    "diversity_weight": 0.2,
    "engagement_weight": 0.3,
    "excitement_weight": 0.3,
    "content_weight": 0.2
}

def extract_highlights(episode: Episode) -> List[Highlight]:
    """提取高光时刻"""
    segments = episode.transcription.segments

    scores = []
    for seg in segments:
        # 兴奋度评分
        excitement = calculate_excitement(seg.audio)

        # 内容重要性评分
        content = calculate_content_importance(seg.text)

        # 互动评分（基于评论时间戳）
        engagement = calculate_engagement(seg.timestamp)

        # 综合评分
        score = (
            HIGHLIGHT_CONFIG["excitement_weight"] * excitement +
            HIGHLIGHT_CONFIG["content_weight"] * content +
            HIGHLIGHT_CONFIG["engagement_weight"] * engagement
        )

        scores.append(SegmentScore(segment=seg, score=score))

    # 排序和去重
    sorted_segments = sorted(scores, key=lambda x: x.score, reverse=True)
    highlights = merge_overlapping(sorted_segments[:20])

    return highlights
```

## 检查清单

- [ ] 多维评分
- [ ] 兴奋度准确
- [ ] 内容重要
- [ ] 去重有效
- [ ] 排序合理
- [ ] 描述准确

## 红牌警告

- 评分权重不当
- 兴奋度误判
- 内容重复
- 忽略重要片段
- 时间戳不准
