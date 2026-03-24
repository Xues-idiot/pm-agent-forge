# Sigma 自主扩展循环

> 核心理念：Sigma 是一个活的框架，通过持续学习和结构化扩展变得更强

---

## Sigma 代号说明

**Sigma (Σ)**：希腊字母，意为"汇总"、"求和"。
目标：汇聚各种 Agent 开发最佳实践，成为开发 AI Agent 的标准工具箱。

---

## 循环哲学

```
研究 → 理解 → 选择 → 扩展 → 验证
  ↑                          ↓
  ← ← ← ← ← ← ← ← ← ← ← ← ←
```

**原则**：
- 研究深度 > 扩展广度
- 做少但做精
- 每轮聚焦一个领域
- 边做边反思

---

## 执行步骤

### 第1步：明确上下文

打开 README.md，确认：
- Sigma 的定位是"Agent 开发框架"
- 核心提供：Skills、Agents、Workflows、Templates
- 目标用户：Coding Agent 开发者

### 第2步：回顾参考架构

快速重温三个核心参考的模式：

| 参考项目 | 核心学到的 |
|---------|-----------|
| superpowers | Skills frontmatter 格式、红牌警告、TDD 思维 |
| deepagents | Middleware 可插拔架构、Agent 状态管理 |
| everything-claude-code | 28 Agent 系统、Continuous Learning |

### 第3步：选择一个领域

从待扩展列表选择一个，或自主发现新方向：

```
优先扩展：
├── P1: 客服 Agent（对话、FAQ、工单）
├── P1: 数据分析 Agent（处理、可视化、报告）
└── P2: 教育 Agent（课程、测评、学习追踪）

自主发现方向：
├── 金融 Agent（风控、投资、理财）
├── 医疗 Agent（问诊、病历、健康管理）
├── 物联网 Agent（设备管理、监控、自动化）
└── 法务 Agent（合同、合规、知识产权）
```

**选择标准**：
- 有真实需求
- 有参考项目可学习
- 能形成 3+ Skills

### 第4步：深度研究

搜索并研究该领域的最佳实践：

**必做**：
- [ ] GitHub 搜索该领域 Agent 项目（star 多优先）
- [ ] 克隆 1-2 个核心项目
- [ ] 阅读 README、SKILL.md、agents/*.md
- [ ] 提炼该领域的核心概念和工作流

**输出**：
```markdown
## [领域] 研究报告

### 核心概念
- 概念1：
- 概念2：

### 常用模式
- 模式1：
- 模式2：

### 代表项目
- [项目名](url) - 特点

### 可借鉴的设计
- 设计1：
- 设计2：
```

### 第5步：评估与选择

在动手前自问：

| 问题 | 回答指南 |
|------|---------|
| 该领域是否有成熟实践？ | 有 → 学习借鉴；无 → 谨慎创新 |
| 现有 Skills 能覆盖吗？ | 能 → 扩展而非新建；不能 → 新建 |
| 这个领域对 Sigma 有价值吗？ | 有 → 继续；无 → 换一个 |
| 能做出 3+ 有质量的 Skills？ | 能 → 继续；不能 → 缩小范围 |

**如果答案不明确，返回第3步换一个领域**

### 第6步：设计 Skills 结构

根据研究结果，设计该领域的 Skills：

```markdown
skills/[领域]/
├── concept/SKILL.md      # 核心概念（如：客服对话流程）
├── skill-A/SKILL.md      # 技能1
├── skill-B/SKILL.md      # 技能2
└── skill-C/SKILL.md      # 技能3
```

**每个 Skill 要素**：
- YAML frontmatter（name + description）
- Overview（1-2 句话）
- 何时使用（触发条件）
- 执行流程（步骤）
- 模板/示例
- 检查清单
- 红牌警告

### 第7步：实现扩展

创建文件：

**必做**：
- [ ] 3-5 个 Skills
- [ ] 1 个 Agent 模板
- [ ] 相关 Workflow（可选）

**执行时**：
- 遵循 Sigma 的 SKILL.md 格式
- 参考 superpowers 的红牌警告风格
- 使用 agent-spec-template.md（如需要）

### 第8步：质量自检

创建后检查：

- [ ] 所有 Skills 有 YAML frontmatter
- [ ] description 以 "Use when" 开头
- [ ] 每个 Skill 有"何时使用"章节
- [ ] 每个 Skill 有执行流程
- [ ] 每个 Skill 有检查清单
- [ ] 每个 Skill 有红牌警告
- [ ] 内容具体可执行（非空洞理论）

**如果有不满足，返回补全**

### 第9步：更新文档

更新 README.md：
```markdown
## [领域] Skills（v1.0）

新增时间：
参考项目：

### 包含内容
- skills/[领域]/：3 个 Skills
- agents/[领域]-agent.md：1 个 Agent

### 核心概念
[2-3 句话描述该领域]
```

### 第10步：Git 提交

```bash
git add -A
git commit -m "feat([领域]): 新增 [领域] Skills 和 Agent

- 新增 skills/[领域]/ (3个Skills)
- 新增 agents/[领域]-agent.md
- 参考: [参考项目名]

循环第 N 轮"
git push
```

---

## 循环控制

### 开始新循环

完成第10步后：
1. 返回第3步
2. 从待扩展列表选择下一个领域
3. 继续执行

### 终止条件

**主动终止**（达到目标）：
- 已覆盖 3+ 个新领域
- 用户说"可以了"或"满意了"

**被动终止**（研究无果）：
- 第4步找不到有价值的研究材料
- 第5步评估后选择放弃
- 连续 2 个领域评估不通过

### 记录循环

每轮结束时简单记录：
```markdown
## 循环记录

| 轮次 | 领域 | 结果 | 备注 |
|------|------|------|------|
| 1 | 客服 | ✅ 完成 | 参考了 XXX |
| 2 | 数据分析 | ✅ 完成 | 参考了 YYY |
| 3 | - | 跳过 | 无足够研究材料 |
| 4 | 教育 | ✅ 完成 | 参考了 XXX |
| 5 | 金融 | ✅ 完成 | 参考了 XXX |
| 6 | HR | ✅ 完成 | 参考了 XXX |
| 7 | IoT | ✅ 完成 | 参考了 XXX |
| 8 | 医疗 | ✅ 完成 | 参考了 XXX |
| 9 | 法律 | ✅ 完成 | 参考了 XXX |
| 10 | PM Skills | ✅ 完成 | +ab-testing, pricing, story-mapping |
| 11 | Customer Service | ✅ 完成 | +escalation, chatbot, quality |
| 12 | PM & Ops | ✅ 完成 | +社群,会员,裂变,KOL |
| 13 | Data+Finance+HR | ✅ 完成 | +data-quality,dashboard,budget,onboarding |
| 14 | Education+IoT+Medical | ✅ 完成 | +student-retention,predictive,telemedicine |
| 15 | Legal+Finance+Education | ✅ 完成 | +ip-management,employment-dispute,tax-planning,certification |
| 16 | PM+HR+Medical+IoT | ✅ 完成 | +gtm,compensation,pharmacy,energy |
| 17 | PM增长+私域复盘+Data治理+Finance成本+HR组织 | ✅ 完成 | +user-growth,campaign-review,data-governance,cost-management,org-design |
| 18 | IoT设备选型+Medical医保+Education在线+Legal合同管理 | ✅ 完成 | +device-selection,insurance-settlement,online-course,contract-management |
| 19 | 私域引流+客服质检+IoT安全+Finance资金管理 | ✅ 完成 | +traffic-acquisition,intelligent-qa,security,treasury-management |
| 20 | PM数据分析+私域转化+DataPipeline+HR招聘 | ✅ 完成 | +product-analytics,conversion-optimization-v2,data-pipeline,recruitment |
| 21 | PM优先级反馈+私域活动变现+客服投诉主动 | ✅ 完成 | +requirement-prioritization,feedback-management,community-event,monetization,complaint-handling,proactive-service |
| 22 | PM画像埋点+HR人才离职+Data用户画像 | ✅ 完成 | +user-portrait,tracking-design,talent-assessment,offboarding,user-portrait |
| 23 | 工程Skills补全+从Pi/Nu学习 | ✅ 完成 | +coding-standards,debugging,agent-workflow,ai-health-check,code-review + pm-frameworks,four-risks,four-fits,growth-loops,pmf-survey + user-stratification,ab-testing,timing-optimization |
| 24 | PM竞品情报+私域直播+客户开发+门店运营 | ✅ 完成 | +competitive-intelligence,customer-development,live-stream-operation,store-operation |
| 25 | PM战略分析+社群守卫运营+Strategy分析+社区运营 | ✅ 完成 | +strategy-analysis,community-guard-operation |
| 26 | PM产品规划+用户留存+用户生命周期 | ✅ 完成 | +product-planning,user-retention,user-lifecycle |
| 27 | PM指标设计+私域KOL管理+反馈管理 | ✅ 完成 | (metrics-design already exists) + kol-management (already exists) + feedback-management (already exists) |
| 28 | PM产品组合+内容营销+定价策略 | ✅ 完成 | +product-portfolio,content-marketing (already exists),pricing-strategy (already exists) |
| 29 | PM产品生命周期+秒杀运营+拼团运营 | ✅ 完成 | +product-lifecycle,seckill-operation (already exists),group-buy-operation (already exists) |
| 30 | PM产品退出+跨部门协作+活动运营 | ✅ 完成 | +product-exit,cross-functional-collaboration,activity-operation |
| 31 | PM数据可视化+小程序运营+私域运营 | ✅ 完成 | +data-visualization,mini-program-operation,private-domain-operations |
| 32 | PM产品实验+客户关系管理 | ✅ 完成 | +product-experimentation,customer-relationship |
| 33 | 工程Skills扩展(从三个项目学习) | ✅ 完成 | +article-writing,backend-patterns,frontend-patterns,deep-research,documentation-lookup,e2e-testing,verification-loop,content-engine,market-research |
| 34 | 审计重复Skills | ✅ 完成 | 审计duplicate skills |
| 35 | PM用户旅程+NPS管理 | ✅ 完成 | +user-journey,nps-management |
| 36 | 私域关键时刻营销 | ✅ 完成 | +moments-marketing |
| 37 | 客服服务质量+智能路由 | ✅ 完成 | +service-quality,intelligent-routing |
| 38 | 数据预测+IoT系统集成 | ✅ 完成 | +predictive-analytics,system-integration |
| 39 | 投资管理+员工留存 | ✅ 完成 | +investment-management,employee-retention |
| 40 | 在线学习+患者体验 | ✅ 完成 | +online-learning,patient-experience |
| 41 | Finance法律扩展 | ✅ 完成 | +tax-planning,treasury-management,contract-management |
| 42 | IoT医学扩展 | ✅ 完成 | +energy-management,device-selection,insurance-settlement,pharmacy-management |
| 43 | PM增长+法律IP扩展 | ✅ 完成 | +gtm-strategy,user-growth,ip-management,employment-dispute,certification-management |
| 44 | PM+运营扩展 | ✅ 完成 | +product-ops,market-analysis,business-model,content-operations,channel-operations,seo-operations,growth-operations,brand-operations,user-operations |
| 45 | 数据+运营扩展 | ✅ 完成 | +data-operations,product-operations,funnel-analysis,cohort-analysis,customer-insights,knowledge-management,recruitment-operations |
| 46 | Finance+Education+IoT+Medical+Legal扩展 | ✅ 完成 | +financial-analysis,learning-optimization,edge-computing,health-data-analysis,compliance-management,mini-program-ecology |
| 47 | 工程Skills扩展 | ✅ 完成 | +database-design,performance-optimization,microservices,devops,testing |
| 48 | 工程Skills扩展v2 | ✅ 完成 | +cloud-architecture,data-engineering,observability |
| 49 | 运营Skills扩展 | ✅ 完成 | +campaign-operation,content-operation,user-operation |
| 50 | 专业化运营Skills | ✅ 完成 | +growth-hacking,community-operation,channel-operation |
| 51 | 工程Skills扩展v3 | ✅ 完成 | +security,message-queue,configuration |
| 52 | PM Skills扩展 | ✅ 完成 | +product-roadmap,product-strategy,product-research |
| 53 | 数据+客服Skills扩展 | ✅ 完成 | +data-mining,customer-feedback,customer-journey |
| 54 | HR Skills扩展 | ✅ 完成 | +talent-management,performance-management,team-building |
| 55 | Finance Skills扩展 | ✅ 完成 | +financial-planning,cost-control |
| 56 | Common Skills扩展 | ✅ 完成 | +presentation,documentation |
| 57 | Marketing+多领域扩展 | ✅ 完成 | +paid-advertising,social-media-marketing,email-marketing,affiliate-marketing,viral-marketing,influencer-marketing,content-marketing,marketing-analytics,caching-strategy,distributed-system,load-balancing,service-mesh,event-driven-architecture,sensor-integration,firmware-development,telehealth,medical-imaging,contract-automation,legal-document-analysis,adaptive-learning,exam-design,due-diligence,employee-engagement,workforce-planning,customer-retention,anomaly-detection,data-modeling,decision-making,critical-thinking |
| 58 | 投研Skills基础(1-11) | ✅ 完成 | +stock-data-collection,financial-statement-analysis,industry-research,company-valuation,research-report-generation,a-share-market-analysis,announcement-analysis,industry-chain-analysis,macro-analysis,technical-analysis,peer-comparison,portfolio-construction |
| 59 | LangGraph多Agent工作流 | ✅ 完成 | +multi-agent-coordination,state-management,conditional-routing,parallel-execution,error-handling,stock-data-api |
| 60 | 投资策略分析 | ✅ 完成 | +value-investment,growth-investment,event-driven-investment |
| 61 | 风险管理与量化 | ✅ 完成 | +risk-management,quantitative-screening,backtesting |
| 62 | 行业专精-消费科技医药 | ✅ 完成 | +industry-consumer,industry-technology,industry-medical |
| 63 | 行业专精-金融新能源制造 | ✅ 完成 | +industry-financial,industry-new-energy,industry-manufacturing |
| 64 | 宏观策略与研报 | ✅ 完成 | +strategy-macro,research-report-reading,sentiment-monitoring |
| 65 | 港美股与数据监控 | ✅ 完成 | +hongkong-us-stocks,data-visualization,monitoring-alerting |
| 66 | 组合管理与交易 | ✅ 完成 | +portfolio-tracking,rebalancing,trading-integration |
| 67 | Agent优化与持续改进 | ✅ 完成 | +prompt-engineering,agent-evaluation,continuous-improvement |
```

---

*Sigma 自主扩展循环 | 2026-03-24*
