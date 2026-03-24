# 内容分类 (Content Classification)

## Overview

内容分类是将播客内容按主题、风格、情绪等维度分类的技能。

## 何时使用

- 内容筛选
- 推荐匹配
- 收藏归类
- 分析趋势

## 流程

1. **文本提取**：提取内容文本
2. **特征提取**：提取分类特征
3. **多维分类**：多维度分类
4. **置信度**：评估置信度
5. **标签生成**：生成分类标签
6. **交叉验证**：验证分类准确
7. **持续更新**：根据反馈更新

## 模板

### 分类维度模板
```python
CLASSIFICATION_DIMENSIONS = {
    "topic": {
        "科技", "商业", "人文", "教育", "娱乐", "新闻"
    },
    "style": {
        "访谈", "对话", "单人讲述", "辩论", "问答"
    },
    "mood": {
        "轻松", "严肃", "激励", "治愈", "专业"
    },
    "depth": {
        "入门", "进阶", "深度", "专业"
    },
    "audience": {
        "小白", "从业者", "管理者", "投资人"
    }
}

def classify_episode(transcription: Transcription) -> Classification:
    """分类episode"""
    features = extract_features(transcription.text)

    return Classification(
        topic=predict_topic(features),
        style=predict_style(features),
        mood=predict_mood(features),
        depth=predict_depth(features),
        audience=predict_audience(features),
        confidence=calculate_confidence(features)
    )
```

## 检查清单

- [ ] 分类准确
- [ ] 多维覆盖
- [ ] 置信度合理
- [ ] 可解释
- [ ] 更新及时
- [ ] 一致性

## 红牌警告

- 分类错误
- 维度缺失
- 置信度失准
- 不一致
- 过于主观
