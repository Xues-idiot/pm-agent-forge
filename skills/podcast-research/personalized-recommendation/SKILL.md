# 个性化推荐 (Personalized Recommendation)

## Overview

个性化推荐是基于用户偏好推荐播客内容的技能。

## 何时使用

- 个性化推荐
- 冷启动推荐
- 相似内容推荐
- 订阅推荐

## 流程

1. **用户画像**：构建用户画像
2. **内容理解**：理解内容特征
3. **偏好学习**：学习用户偏好
4. **相似度计算**：计算相似度
5. **推荐生成**：生成推荐列表
6. **解释生成**：生成推荐理由
7. **反馈处理**：处理用户反馈

## 模板

### 推荐系统配置
```python
RECOMMENDATION_CONFIG = {
    "model": "collaborative_filtering",
    "num_candidates": 100,
    "num_final": 10,
    "diversity": 0.3
}

async def recommend(user_id: str, limit: int = 10) -> List[Recommendation]:
    """个性化推荐"""
    # 获取用户历史
    user_history = get_user_history(user_id)

    # 获取用户偏好
    user_prefs = get_user_preferences(user_id)

    # 候选生成
    candidates = generate_candidates(user_prefs, limit=100)

    # 排序
    scored = []
    for candidate in candidates:
        score = calculate_relevance(candidate, user_prefs)
        explanation = generate_explanation(candidate, user_prefs)
        scored.append(Recommendation(
            item=candidate,
            score=score,
            explanation=explanation
        ))

    # 多样性排序
    sorted_recs = sort_by_diversity(scored, diversity=0.3)

    return sorted_recs[:limit]
```

## 检查清单

- [ ] 用户画像准确
- [ ] 偏好学习
- [ ] 推荐准确
- [ ] 多样性
- [ ] 解释合理
- [ ] 反馈更新

## 红牌警告

- 冷启动问题
- 推荐不准确
- 多样性不足
- 解释不相关
- 反馈不更新
