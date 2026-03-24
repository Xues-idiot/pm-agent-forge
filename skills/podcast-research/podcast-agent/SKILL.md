# 播客研究Agent (Podcast Research Agent)

## Overview

播客研究Agent是基于LangGraph的多Agent播客研究系统。自动化完成播客发现、内容分析、洞察挖掘、报告生成全流程。

## Agent概述

```
podcast-research-agent
├── supervisor (调度Agent)
│   └── 理解需求、分解任务、协调Agent
├── discovery-agent (发现Agent)
│   └── 搜索、筛选、订阅播客
├── collection-agent (采集Agent)
│   └── 下载、转写、元数据处理
├── analysis-agent (分析Agent)
│   └── 主题、洞察、分类分析
└── report-agent (报告Agent)
    └── 聚合、生成、格式化报告
```

## 核心Skills

| Skill | 用途 |
|-------|------|
| podcast-discovery | 播客发现 |
| episode-collection | Episode采集 |
| transcription | 语音转写 |
| speaker-extraction | 说话人提取 |
| topic-extraction | 主题提取 |
| summary-generation | 摘要生成 |
| key-moment-extraction | 关键时刻提取 |
| content-classification | 内容分类 |
| guest-extraction | 嘉宾提取 |
| insight-mining | 洞察挖掘 |
| cross-episode-analysis | 跨Episode分析 |
| research-report | 研究报告生成 |

## 工作流程

```
用户输入研究主题
    ↓
Supervisor分解任务
    ↓
┌─────────────────────────────────┐
│  Discovery Agent → 找到相关播客  │
│  Collection Agent → 采集转写    │
│  Analysis Agent → 分析内容洞察  │
└─────────────────────────────────┘
    ↓
Report Agent聚合生成报告
    ↓
输出研究报告
```

## 使用示例

```python
# 研究请求
request = {
    "task": "研究AI创业投资",
    "topics": ["AI", "创业", "投资"],
    "num_podcasts": 5,
    "report_type": "detailed"
}

# 执行研究
result = await podcast_graph.invoke(request)
print(result["report"])
```

## 扩展方向

- [ ] 多语言翻译
- [ ] 社交分享集成
- [ ] 播客制作辅助
- [ ] 持续追踪
- [ ] 对话式交互
