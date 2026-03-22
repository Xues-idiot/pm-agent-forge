# PM-Agent-Forge

> 帮助 Coding Agent 更好地开发 PM Agent 和私域运营 Agent 的框架

## 核心理念

Sigma 是一个帮助 Coding Agent 更好地开发 AI Agent 的框架，名字取自希腊字母 Σ，意为"汇总"。

核心问题：Coding Agent 很强大，但缺乏结构化的开发方法和专业领域知识。

解决方案：提供 Skills（技能）、Agents（子代理）、Workflows（工作流），让 Coding Agent 在开发任何 AI Agent 时都有章可循。

## 项目结构

```
pm-agent-forge/
├── skills/                    # Skills 技能库（按领域组织）
│   ├── pm/                   # 产品经理技能
│   ├── private-ops/          # 私域运营技能
│   ├── common/               # 通用技能
│   ├── meta/                 # 元技能
│   ├── customer-service/      # 客服技能
│   ├── data-analytics/       # 数据分析技能
│   ├── education/            # 教育技能
│   ├── finance/              # 金融技能
│   ├── hr/                  # 人力资源技能
│   ├── iot/                 # 物联网技能
│   ├── medical/             # 医疗技能
│   └── legal/               # 法律技能
├── agents/                   # Subagent 模板
│   ├── research-agent.md
│   ├── prd-writer-agent.md
│   ├── campaign-designer-agent.md
│   ├── analytics-agent.md
│   ├── qa-agent.md
│   ├── customer-service-agent.md
│   ├── data-analytics-agent.md
│   ├── education-agent.md
│   ├── finance-agent.md
│   ├── hr-agent.md
│   ├── iot-agent.md
│   └── medical-agent.md
├── workflows/                # 工作流
├── templates/                # 文档模板
└── docs/                    # 文档
```

## 三大核心机制

### 1. Skills 系统

Skills 是触发式的专业技能模块，自动基于上下文激活：

```yaml
---
name: pm-prd-writing
description: Use when writing or reviewing PRD documents
---
```

每个 Skill 包含：
- YAML frontmatter（name + description）
- 何时使用（触发条件）
- 具体执行流程
- 模板和示例
- 检查清单
- 红牌警告

### 2. Agents 系统

针对不同任务的专用子代理：

| Agent | 用途 | 模型 |
|-------|------|------|
| research-agent | 信息调研 | Opus |
| prd-writer-agent | PRD 写作 | Opus |
| campaign-designer-agent | 营销活动设计 | Opus |
| analytics-agent | 数据分析 | Sonnet |
| qa-agent | 质量保证 | Sonnet |
| customer-service-agent | 客服支持 | Sonnet |
| data-analytics-agent | 数据分析 | Sonnet |
| education-agent | 教育培训 | Sonnet |
| finance-agent | 金融分析 | Sonnet |
| hr-agent | 人力资源 | Sonnet |
| iot-agent | 物联网 | Sonnet |
| medical-agent | 医疗辅助 | Sonnet |
| legal-agent | 法律服务 | Sonnet |

### 3. PM Skills（产品经理技能）

| Skill | 用途 |
|-------|------|
| prd-writing | PRD 写作 |
| user-research | 用户研究 |
| competitive-analysis | 竞品分析 |
| market-insight | 市场洞察 |
| roadmap-writing | 路线图制定 |
| feature-spec | 功能规格 |
| metrics-design | 指标体系设计 |
| ab-testing | A/B测试 |
| pricing-strategy | 定价策略 |
| user-story-mapping | 用户故事地图 |
| gtm-strategy | 市场进入 |
| user-growth | 用户增长 |
| product-analytics | 产品分析 |
| requirement-prioritization | 需求优先级 |
| feedback-management | 用户反馈管理 |

### 4. Private Ops Skills（私域运营技能）

| Skill | 用途 |
|-------|------|
| campaign-design | 活动策划 |
| rfm-analysis | RFM分析 |
| content-strategy | 内容策略 |
| 转化优化 | 转化优化 |
| community-operation | 社群运营 |
| membership-system | 会员体系 |
| fission-campaign | 裂变活动 |
| kol-management | KOL管理 |
| campaign-review | 活动复盘 |
| traffic-acquisition | 私域引流 |
| conversion-optimization | 转化优化(v2) |
| community-event | 社群活动 |
| monetization | 私域变现 |

### 5. Customer Service Skills（客服技能）

| Skill | 用途 |
|-------|------|
| faq-handling | FAQ 检索和回复 |
| ticket-routing | 智能工单分配 |
| sentiment-analysis | 情感检测 |
| response-drafting | 回复起草 |
| knowledge-base-search | 知识库搜索 |
| escalation-management | 升级处理 |
| chatbot-script | 对话脚本 |
| quality-assurance | 服务质量 |
| intelligent-qa | 智能质检 |
| complaint-handling | 投诉处理 |
| proactive-service | 主动服务 |

### 6. Data Analytics Skills（数据分析技能）

| Skill | 用途 |
|-------|------|
| data-processing | 数据清洗转换 |
| visualization-creation | 可视化创建 |
| report-generation | 报告生成 |
| metric-calculation | 指标计算 |
| data-quality | 数据质量 |
| dashboard-design | 看板设计 |
| data-governance | 数据治理 |
| data-pipeline | 数据流水线 |

### 7. Education Skills（教育技能）

| Skill | 用途 |
|-------|------|
| course-design | 课程设计 |
| learning-assessment | 学习评估 |
| learning-progress-tracking | 进度追踪 |
| content-creation | 内容创作 |
| student-retention | 学员留存 |
| certification-management | 证书管理 |
| online-course | 在线课程 |

### 8. Finance Skills（金融技能）

| Skill | 用途 |
|-------|------|
| risk-assessment | 风险评估 |
| investment-analysis | 投资分析 |
| financial-report-analysis | 财务报告分析 |
| compliance-check | 合规检查 |
| budget-management | 预算管理 |
| tax-planning | 税务筹划 |
| cost-management | 成本管理 |
| treasury-management | 资金管理 |

### 9. HR Skills（人力资源技能）

| Skill | 用途 |
|-------|------|
| resume-screening | 简历筛选 |
| performance-evaluation | 绩效评估 |
| employee-training | 员工培训 |
| job-description-writing | JD 撰写 |
| employee-onboarding | 入职管理 |
| compensation-design | 薪酬设计 |
| organizational-design | 组织设计 |
| recruitment | 招聘管理 |

### 10. IoT Skills（物联网技能）

| Skill | 用途 |
|-------|------|
| device-management | 设备管理 |
| monitoring-alerting | 监控告警 |
| data-collection | 数据采集 |
| automation-rules | 自动化规则 |
| predictive-maintenance | 预测性维护 |
| energy-management | 能源管理 |
| device-selection | 设备选型 |
| security | IoT安全 |

### 11. Medical Skills（医疗技能）

| Skill | 用途 |
|-------|------|
| medical-record-analysis | 病历分析 |
| diagnostic-assistance | 诊断辅助 |
| health-management | 健康管理 |
| medical-literature-search | 文献检索 |
| telemedicine | 远程医疗 |
| pharmacy-management | 药房管理 |
| insurance-settlement | 医保结算 |

### 12. Legal Skills（法律技能）

| Skill | 用途 |
|-------|------|
| contract-review | 合同审查 |
| legal-research | 法律研究 |
| compliance-check | 合规检查 |
| risk-assessment | 法律风险评估 |
| ip-management | 知识产权管理 |
| employment-dispute | 劳动争议 |
| contract-management | 合同管理 |

### 12. Workflows 系统

```
brainstorming → planning → executing → reviewing → evolving
```

每个 Workflow 定义了完成特定类型任务的标准化流程。

## 设计理念

### 来自 Superpowers 的借鉴
- Skills 触发机制
- RED-GREEN-REFACTOR TDD 循环
- 两阶段 Review（规格合规 → 代码质量）
- Git Worktree 并行开发

### 来自 Deep Agents 的借鉴
- create_deep_agent() 返回 LangGraph StateGraph
- Middleware 栈架构
- SkillsMiddleware 支持外部 Skills 注入

### 来自 Everything Claude Code 的借鉴
- 28 专业 Subagent 系统
- 116 Skills 覆盖领域
- Continuous Learning 持续学习机制

## 使用方法

### 安装

```bash
# 克隆仓库
git clone https://github.com/Xues-idiot/pm-agent-forge.git

# 或作为 submodule
git submodule add https://github.com/Xues-idiot/pm-agent-forge.git
```

### 在项目中使用

```
# 复制 skills 到项目
cp -r pm-agent-forge/skills <your-project>/skills

# 复制 agents 到项目
cp -r pm-agent-forge/agents <your-project>/agents
```

### 触发 Skills

当 Coding Agent 遇到相关上下文时，会自动触发对应的 Skill：
- PRD 相关 → 触发 pm-prd-writing
- 用户调研 → 触发 pm-user-research
- 竞品分析 → 触发 pm-competitive-analysis
- ...

## 质量标准

参考 Superpowers 的写作风格：

| 要素 | 要求 |
|------|------|
| **结构清晰** | Overview / When to Use / How it Works / 红牌警告 |
| **具体可执行** | 步骤明确，模板可复制 |
| **好/坏对比** | 展示正确和错误示例 |
| **红牌警告** | 告诉什么时候该停止 |

## 贡献指南

### 创建新 Skill

1. 在 `skills/<领域>/` 下创建目录
2. 创建 `SKILL.md` 文件
3. 使用 skills-writing 的模板
4. 更新 README.md

### 创建新 Agent

1. 在 `agents/` 下创建 `<name>-agent.md`
2. 使用 YAML frontmatter
3. 定义角色和执行流程
4. 更新 README.md

### 提交规范

```
[技能/代理/工作流]: 完成了什么

参考了：xxx 项目
原因：xxx
```

## License

MIT
