# 关键时刻提取 (Key Moment Extraction)

## Overview

关键时刻提取是识别播客中高光片段的技能。用于快速跳转、精彩片段、社交分享。

## 何时使用

- 快速预览精彩片段
- 制作精彩集锦
- 社交媒体分享
- 时间戳导航

## 流程

1. **兴奋度分析**：分析语音兴奋度
2. **关键词检测**：检测关键词/主题词
3. **笑声/掌声检测**：检测高光时刻
4. **结构分析**：分析内容结构
5. **时间戳生成**：生成时间戳
6. **片段剪辑**：剪辑高光片段
7. **描述生成**：生成片段描述

## 模板

### 高光检测模板
```python
def extract_key_moments(transcription: Transcription) -> List[KeyMoment]:
    """提取关键时刻"""
    moments = []

    # 兴奋度检测
    excitement = detect_excitement(transcription.audio)

    # 笑声检测
    laughter = detect_laughter(transcription.audio)

    # 结构识别（自我介绍、总结、金句等）
    structure = detect_structure(transcription.segments)

    # 合并高光
    all_moments = excitement + laughter + structure
    moments = merge_overlapping(all_moments)

    # 排序和过滤
    return sorted(moments, key=lambda x: x.score, reverse=True)[:10]

@dataclass
class KeyMoment:
    start_time: float
    end_time: float
    score: float
    type: str  # excitement/laughter/quote/intro/outro
    description: str
```

## 检查清单

- [ ] 检测准确
- [ ] 时间戳精确
- [ ] 类型多样
- [ ] 描述准确
- [ ] 片段完整
- [ ] 排序合理

## 红牌警告

- 漏检重要时刻
- 时间戳不准
- 误检噪音
- 片段不完整
- 描述不准确
