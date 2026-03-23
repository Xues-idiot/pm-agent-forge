---
name: pm-frameworks
description: Use when applying product management frameworks, making strategic decisions, prioritization, planning, or assessing product-market fit. Covers discovery, growth, planning, measurement frameworks and AI-era practices.
---

# PM Frameworks

产品管理框架知识库，涵盖发现、增长、规划、度量框架和AI时代实践。

## 何时使用

- **Discovery**: 功能验证、用户研究、假设测试、"该不该做这个？"
- **Growth**: 获取、留存、病毒式增长、增长飞轮、产品驱动增长
- **Planning**: 路线图、优先级、Now-Next-Later、LNO框架
- **Measurement**: PMF调查、指标、成功标准
- **AI Products**: Evals、Fine-tuning vs RAG、Prompt工程、AI单位经济
- **Strategy**: Four Fits、市场产品匹配、竞争定位
- **Execution**: PRD、Spec、Issue vs Story、Prototype-First开发

## 核心框架速查

| 框架 | 用途 | 关键问题 |
|------|------|----------|
| Four Risks | 风险评估 | 能做吗？用户要吗？商业上值吗？ |
| Four Fits | 市场匹配 | 产品-市场/渠道/模型匹配？ |
| Growth Loops | 增长机制 | 怎么形成正向循环？ |
| Now-Next-Later | 规划路线图 | 现在/下一步/以后做什么？ |
| LNO | 优先级 | 杠杆/中性/开销？ |
| PMF Survey | 产品市场匹配 | 用户有多失望？ |

---

## Discovery 框架

### Four Risks (Marty Cagan)

评估产品机会的四个风险：

| 风险 | 问题 | 验证方式 |
|------|------|----------|
| **Value Risk** | 用户会买/用这个吗？ | 用户访谈、支付意愿 |
| **Usability Risk** | 用户能搞懂吗？ | 可用性测试 |
| **Feasibility Risk** | 我们能造出来吗？ | 技术评估 |
| **Business Viability Risk** | 对业务有价值吗？ | 商业模型验证 |

**应用问题**：
- "用户说想要这个，但他们真的愿意付钱吗？" → Value Risk
- "这个功能够简单吗，用户一看就懂？" → Usability Risk
- "我们的AI能力能支撑这个功能吗？" → Feasibility Risk
- "这个功能对我们的商业模式有意义吗？" → Business Viability Risk

### Continuous Discovery (Teresa Torres)

持续发现框架：

```
周会用户接触 → 机会解决方案树 → 假设测试 → 小实验 > 大赌注
```

**核心实践**：
- 每周与用户接触
- 构建机会解决方案树
- 持续测试假设
- 小实验 > 大赌注

---

## Growth 框架

### Growth Loops (Elena Verna)

四种增长飞轮：

| 飞轮类型 | 机制 | 示例 |
|----------|------|------|
| **Viral** | 用户邀请用户 | Dropbox推荐 |
| **Content/SEO** | 内容吸引用户 | 博客文章 |
| **Network Effect** | 用户越多越有价值 | 微信 |
| **Paid** | 收入资助获客 | SaaS订阅 |

**Growth Loop 分析模板**：
```markdown
## Growth Loop 分析

### 当前飞轮
- 类型: [Viral/Content/Network/Paid]
- 驱动因素: [什么让飞轮转动]
- 瓶颈: [什么限制增长]

### 优化建议
1. [加强飞轮的方法]
2. [消除瓶颈的方法]
```

### Four Fits (Brian Balfour)

四种匹配度：

| 匹配 | 问题 | 检查清单 |
|------|------|----------|
| **Market-Product** | 产品满足市场需求？ | 用户访谈、PMF分数 |
| **Product-Channel** | 产品适合获客渠道？ | 渠道转化率 |
| **Channel-Model** | 渠道和商业模式匹配？ | CAC vs LTV |
| **Model-Market** | 商业模式适合市场？ | 单元经济 |

### Product-Led Growth

产品驱动增长策略：

- Self-serve to sales-assist递进
- 基于使用量的资格认定
- 扩张收入模式

---

## Planning 框架

### Now-Next-Later (Janna Bastow)

 Roadmap规划框架：

```
Now (当前)          → Next (1-3月)      → Later (未来)
高置信度             中置信度              低置信度
当前冲刺             明确但可能有变         探索性可能
```

**应用**：
- "这个功能确定要做吗？" → Now
- "我们想做但还没承诺" → Next
- "如果资源充足可以考虑" → Later

### LNO Prioritization (Shreyas Doshi)

优先级分类框架：

| 类别 | 定义 | 行动 |
|------|------|------|
| **Leverage** | 高影响力 | 优先做 |
| **Neutral** | 预期工作 | 批量安排 |
| **Overhead** | 低价值 | 最小化或消除 |

**评估问题**：
- 如果不做这个，杠杆工作会受损吗？
- 这个是中性工作还是开销？

### Scope Projects Down

范围缩减原则：

- 功能80/20原则
- 最小可行范围
- 狠心裁剪，之后再加

---

## Measurement 框架

### PMF Survey (Rahul Vohra)

产品市场匹配度调查：

**核心问题**：
> "如果你不能使用这个产品，你会多失望？"
> - 非常失望 (40%+ 是目标)
> - 有点失望
> - 不失望

**行动**：
- 找到高期望用户（40%+非常失望）
- 为他们构建
- 忽略其他人

### AI Unit Economics

AI功能单位经济：

```markdown
## AI单位经济分析

### 成本
| 项目 | 单次成本 | 日成本 | 月成本 |
|------|----------|--------|--------|
| LLM调用 | $0.001 | $X | $X |
| API成本 | $0.0001 | $X | $X |
| **总计** | $0.0011 | $X | $X |

### 价值
- 用户愿意为这个功能付多少？
- 功能月活用户数？
- 目标LTV？

### 结论
- 盈利 / 亏损 / 平衡点
```

---

## AI-Era 实践

### Prototype-First (Aakash Gupta)

AI时代开发流程：

```
旧流程（线性）: PRD → 设计 → 开发 → 测试
新流程（循环）: 想法 → 快速原型 → PRD → 优化原型 → 交付
```

**原则**：
- 原型先于文档
- 代码即规格
- 迭代快于文档

### Issues Not Stories (Linear)

用Issue而非Story：

- 描述问题，而非解决方案
- 让工程师思考如何做
- 方向 → 构建 → 质量阶段

### AI Evals (Aman Khan)

AI评估层次：

| 层级 | 测试什么 | 示例 |
|------|----------|------|
| **Prompt-level** | 单个Prompt效果 | 对话质量 |
| **Task-level** | 任务完成度 | 提取信息准确率 |
| **System-level** | 系统集成 | 端到端流程 |
| **Regression** | AI回归 | Prompt变更后质量 |

---

## 框架应用对话模板

**不要这样说**：
> "让我解释一下Four Risks框架..."

**要这样说**：
> "你有什么证据证明用户想要这个？那就是Value Risk。"

**追问问题**：
- "这周你能测试的最小东西是什么？" (Continuous Discovery)
- "这是杠杆、中性还是开销工作？" (LNO)
- "能在写PRD前先原型吗？" (Prototype-First)
- "你的增长飞轮是什么？" (Growth Loops)

---

## 检查清单

### 决策前检查
- [ ] 评估了Four Risks？
- [ ] 找到了高期望用户？
- [ ] 定义了成功指标？
- [ ] 考虑了增长飞轮？

### 规划前检查
- [ ] 使用Now-Next-Later？
- [ ] 区分了Leverage/Neutral/Overhead？
- [ ] 范围缩减到最小可行？

### 发布前检查
- [ ] PMF分数>40%？
- [ ] 成本模型建立？
- [ ] 监控指标定义？

---

## 红牌警告

- 不验证假设就开发
- 跳过用户访谈
- 用内部讨论代替用户测试
- 大赌注代替小实验
- 观点>证据

## 好/坏对比

**好**：
```
用户说想要AI推荐功能。
→ 先做一个小原型让用户测试
→ 收集数据验证假设
→ 根据反馈迭代
```

**坏**：
```
用户说想要AI推荐功能。
→ 直接开发完整推荐系统
→ 3个月后上线
→ 发现用户不需要
```
