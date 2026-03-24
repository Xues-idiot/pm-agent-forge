# 新闻资讯垂直浏览器 (News Browser)

## Overview

新闻资讯垂直浏览器是自动化采集和分析新闻内容的技能。

## 何时使用

- 新闻聚合采集
- 舆情监控
- 竞品监控
- 内容分析

## 流程

1. **来源管理**：管理新闻源
2. **增量采集**：增量采集新内容
3. **内容提取**：提取正文内容
4. **分类标签**：自动分类打标签
5. **去重过滤**：去重和过滤
6. **存储索引**：存储建立索引
7. **告警通知**：关键词告警

## 模板

### 新闻采集模板
```python
NEWS_SOURCES = {
    "财经": ["证券时报", "第一财经", "财新"],
    "科技": ["36kr", "虎嗅", "品玩"],
    "综合": ["澎湃", "腾讯新闻", "今日头条"]
}

async def collect_news(keyword: str = None, sources: list = None):
    """采集新闻"""
    all_news = []

    for source in (sources or NEWS_SOURCES["综合"]):
        url = get_source_url(source, keyword)
        await page.goto(url)
        await page.wait_for_selector(".article-list")

        articles = await page.extract_articles(".article-item")
        all_news.extend(articles)

    # 去重
    unique_news = deduplicate(all_news)

    return unique_news
```

## 检查清单

- [ ] 来源可靠
- [ ] 内容完整
- [ ] 增量准确
- [ ] 去重有效
- [ ] 分类准确
- [ ] 告警及时

## 红牌警告

- 来源失效
- 内容不完整
- 重复采集
- 分类错误
- 告警噪音
