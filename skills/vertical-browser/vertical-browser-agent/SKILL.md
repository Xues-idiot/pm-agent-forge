# 垂直浏览器Agent (Vertical Browser Agent)

## Overview

垂直浏览器Agent是基于LangGraph的自动化浏览器操作Agent。针对特定垂直领域（社交媒体、电商、新闻、招聘等）实现智能化浏览器操作。

## Agent架构

```
vertical-browser-agent
├── supervisor (调度Agent)
│   └── 理解任务、协调子Agent
├── navigation-agent (导航Agent)
│   └── 页面导航、元素定位
├── extraction-agent (提取Agent)
│   └── 内容提取、数据清洗
├── interaction-agent (交互Agent)
│   └── 表单填写、点击操作
└── anti-bot-agent (反爬Agent)
    └── 代理管理、验证码处理
```

## 核心Skills

| Skill | 用途 |
|-------|------|
| browser-automation | Playwright/Selenium基础 |
| social-media-browser | 社交媒体操作 |
| e-commerce-browser | 电商操作 |
| news-browser | 新闻采集 |
| recruitment-browser | 招聘操作 |
| content-extraction-enhanced | AI内容提取 |
| anti-anti-bot | 反反爬 |
| form-automation | 表单自动化 |
| data-pipeline | 数据采集管道 |

## 使用示例

```python
# 任务定义
task = {
    "type": "social_media",
    "action": "scrape_posts",
    "target": "x.com/hashtag/AI",
    "limit": 100,
    "fields": ["content", "author", "likes", "retweets"]
}

# 执行
result = await vertical_browser.invoke(task)
```

## 扩展方向

- [ ] 更多垂直场景
- [ ] 多浏览器支持
- [ ] 分布式采集
- [ ] 智能化调度
- [ ] 可视化配置
