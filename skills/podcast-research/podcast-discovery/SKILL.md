# 播客发现 (Podcast Discovery)

## Overview

播客发现是从海量播客中智能筛选目标播客的技能。涵盖主题搜索、排行榜分析、推荐算法、订阅管理等。

## 何时使用

- 寻找特定主题的播客
- 发现优质新播客
- 管理播客订阅列表
- 追踪更新

## 流程

1. **需求分析**：确定收听目标
2. **搜索发现**：多渠道搜索播客
3. **质量评估**：评估播客质量
4. **订阅管理**：订阅优质播客
5. **更新追踪**：追踪新 episodes
6. **归档整理**：整理播客库
7. **效果评估**：评估发现效果

## 模板

### 播客发现配置模板
```python
PODCAST_SOURCES = {
    "apple_podcasts": {"region": "cn", "categories": ["新闻", "商业", "科技"]},
    "spotify": {"regions": ["cn", "us"], "features": ["新上架", "热门"]},
    "xiaoyuzhou": {"topics": ["科技", "创业", "成长"]},
    "qfm": {"topics": ["金融", "投资"]}
}

def discover_podcasts(topic: str, quality_threshold: float = 0.7) -> List[Podcast]:
    # 搜索
    results = search_across_sources(topic)
    # 质量过滤
    filtered = [p for p in results if p.quality_score > quality_threshold]
    # 排序
    return sorted(filtered, key=lambda x: x.relevance_score, reverse=True)
```

## 检查清单

- [ ] 多渠道覆盖
- [ ] 质量评估准确
- [ ] 更新及时
- [ ] 个性化推荐
- [ ] 订阅管理便捷
- [ ] 播放记录同步

## 红牌警告

- 搜索结果不相关
- 质量评估失准
- 更新延迟
- 推荐过于大众化
- 重复推荐
