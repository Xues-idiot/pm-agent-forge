# Investment Research Agent (投研Agent)

> 使用LangGraph构建的A股投研多Agent系统

## Agent概述

投研Agent是一个基于LangGraph的多Agent协作系统，用于自动化完成A股投资研究工作。系统由多个专业子Agent组成，各Agent分工协作，模拟真实券商研究部的运作模式。

## 系统架构

```
investment-research-graph
├── supervisor (调度Agent)
│   ├── 理解研究需求
│   ├── 分解任务
│   └── 协调子Agent
│
├── market-analyst (宏观/市场分析师)
│   ├── 宏观分析
│   ├── A股市场分析
│   └── 板块轮动分析
│
├── industry-analyst (行业分析师)
│   ├── 产业链分析
│   ├── 行业研究
│   └── 景气度判断
│
├── company-analyst (公司分析师)
│   ├── 财务报表分析
│   ├── 公司估值
│   ├── 竞品对比
│   └── 公告解读
│
├── data-agent (数据Agent)
│   ├── 股票数据采集
│   ├── 数据清洗
│   └── 数据存储
│
└── report-agent (报告Agent)
    ├── 研究报告生成
    └── 投资建议输出
```

## 核心Skills

| Skill | 用途 |
|-------|------|
| stock-data-collection | 数据采集 |
| macro-analysis | 宏观分析 |
| a-share-market-analysis | A股市场分析 |
| industry-research | 行业研究 |
| industry-chain-analysis | 产业链分析 |
| financial-statement-analysis | 财务分析 |
| company-valuation | 公司估值 |
| peer-comparison | 竞品对比 |
| announcement-analysis | 公告解读 |
| research-report-generation | 报告生成 |
| technical-analysis | 技术分析 |
| portfolio-construction | 组合构建 |

## Agent Spec

### Supervisor Agent

```yaml
name: investment-research-supervisor
description: 投研任务调度Agent，负责分解任务和协调子Agent
instructions: |
  1. 理解用户投研需求
  2. 将任务分解为子任务
  3. 调用相应子Agent执行
  4. 汇总子Agent结果
  5. 输出最终研究报告

tools:
  - market-analyst
  - industry-analyst
  - company-analyst
  - data-agent
  - report-agent

output:
  - 任务分解计划
  - 研究报告
  - 投资建议
```

### Market Analyst Agent

```yaml
name: market-analyst
description: 宏观和市场分析师，负责宏观经济和A股市场分析
instructions: |
  1. 分析国内外宏观经济
  2. 分析北向资金流向
  3. 判断市场情绪
  4. 分析板块轮动
  5. 给出大盘研判

tools:
  - macro-analysis
  - a-share-market-analysis
  - technical-analysis
  - stock-data-collection

output:
  - 宏观分析报告
  - 市场情绪报告
  - 大盘研判
```

### Industry Analyst Agent

```yaml
name: industry-analyst
description: 行业分析师，负责产业链和行业研究
instructions: |
  1. 分析行业产业链结构
  2. 研究行业发展趋势
  3. 判断行业景气度
  4. 寻找行业投资主线
  5. 给出行业配置建议

tools:
  - industry-chain-analysis
  - industry-research
  - stock-data-collection

output:
  - 产业链图谱
  - 行业研究报告
  - 行业配置建议
```

### Company Analyst Agent

```yaml
name: company-analyst
description: 公司分析师，负责个股深度研究
instructions: |
  1. 分析公司基本面
  2. 解读财务报表
  3. 进行公司估值
  4. 对比竞争对手
  5. 分析重要公告
  6. 给出投资建议

tools:
  - financial-statement-analysis
  - company-valuation
  - peer-comparison
  - announcement-analysis

output:
  - 财务分析报告
  - 估值报告
  - 个股研判
```

### Data Agent

```yaml
name: data-agent
description: 数据Agent，负责数据采集和清洗
instructions: |
  1. 从多种渠道采集数据
  2. 数据清洗和标准化
  3. 数据质量校验
  4. 数据存储和更新

tools:
  - stock-data-collection

output:
  - 清洗后的结构化数据
  - 数据质量报告
```

### Report Agent

```yaml
name: report-agent
description: 报告Agent，负责生成最终研究报告
instructions: |
  1. 收集各分析师结论
  2. 整合分析内容
  3. 生成完整研究报告
  4. 给出投资建议

tools:
  - research-report-generation
  - portfolio-construction

output:
  - 完整研究报告
  - 投资建议
```

## 工作流程

### 单股票研究流程

```
1. 用户输入股票代码/名称
   ↓
2. Supervisor分解任务
   ├── 数据采集 → Data Agent
   ├── 宏观分析 → Market Analyst
   ├── 行业分析 → Industry Analyst
   └── 个股分析 → Company Analyst
   ↓
3. 各Agent并行执行
   ↓
4. Report Agent汇总生成报告
   ↓
5. 输出研究报告和投资建议
```

### 行业研究流程

```
1. 用户输入行业名称
   ↓
2. Supervisor分解任务
   ├── 产业链分析 → Industry Analyst
   ├── 市场数据 → Data Agent
   └── 宏观环境 → Market Analyst
   ↓
3. 各Agent并行执行
   ↓
4. Report Agent汇总生成报告
   ↓
5. 输出行业报告和配置建议
```

## 使用示例

### 研究单只股票

```python
from langchain_core.messages import HumanMessage
from investment_research_graph import research_graph

# 初始化图
graph = research_graph()

# 研究请求
request = {
    "task": "研究贵州茅台",
    "stock_code": "600519",
    "task_type": "stock"
}

# 执行研究
result = graph.invoke(request)
```

### 研究行业

```python
request = {
    "task": "研究新能源汽车行业",
    "industry": "新能源汽车",
    "task_type": "industry"
}

result = graph.invoke(request)
```

## 模型配置

| Agent | 推荐模型 | 用途 |
|-------|---------|------|
| Supervisor | Claude 3.5 Sonnet | 任务调度和协调 |
| Market Analyst | Claude 3.5 Sonnet | 宏观分析 |
| Industry Analyst | Claude 3.5 Sonnet | 行业分析 |
| Company Analyst | Claude 3 Opus | 个股深度分析 |
| Data Agent | Claude 3 Haiku | 数据处理 |
| Report Agent | Claude 3.5 Sonnet | 报告生成 |

## 数据源

- akshare: 行情数据、基金数据
- tushare: 财务数据、公告数据
- 东方财富: 资金流向、研报
- 同花顺: 资讯数据

## 扩展方向

- [ ] 港股/美股研究能力
- [ ] 量化策略信号
- [ ] 实时舆情监控
- [ ] 组合自动跟踪调仓
- [ ] 研报合规检查

## 相关Skills

- [stock-data-collection](../skills/investment-research/stock-data-collection/SKILL.md)
- [financial-statement-analysis](../skills/investment-research/financial-statement-analysis/SKILL.md)
- [industry-research](../skills/investment-research/industry-research/SKILL.md)
- [company-valuation](../skills/investment-research/company-valuation/SKILL.md)
- [research-report-generation](../skills/investment-research/research-report-generation/SKILL.md)
