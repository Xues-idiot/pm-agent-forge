---
name: engineering-ai-health-check
description: Use before shipping AI features. Pre-launch health check that evaluates 6 dimensions: model selection, data quality, cost, monitoring, failure UX, optimization.
---

# AI Health Check

发布AI功能前的健康检查，确保功能Ready to Ship。

## 何时使用

- AI功能开发完成，准备发布
- Sprint结束前检查AI功能
- 上线前评审
- Code Review AI相关功能

## 6维度检查

| 维度 | 重要性 | 检查什么 |
|------|--------|----------|
| **Model Selection** | ⭐⭐⭐ | 是否尝试了简单方案？ |
| **Data Quality** | ⭐⭐⭐⭐⭐ | 最容易被忽视的维度 |
| **Cost Modeling** | ⭐⭐⭐⭐⭐ | 规模化的成本可控吗？ |
| **Monitoring** | ⭐⭐⭐⭐ | 如何知道它坏了？ |
| **Failure UX** | ⭐⭐⭐⭐⭐ | AI搞砸时用户体验？ |
| **Optimization** | ⭐⭐⭐ | 指标测对了吗？ |

## 判决逻辑

| 条件 | 判决 |
|------|------|
| 任何 Blocker | **不要发布** |
| 2+ Risks（无Blocker） | **需要改进** |
| 0-1 Risks | **Ready** |

---

## D1: Model Selection

**检查问题：**
- 是否对比了简单方案（规则、查找表）？
- 为什么选择当前模型？
- 模型尺寸是否合适？
- 是否考虑了延迟要求？

**评估标准：**

| 状态 | 说明 |
|------|------|
| Ready | 尝试了简单方案，当前模型有明确优势 |
| Risk | 简单方案未充分尝试 |
| Blocker | 选择过大/过贵模型，无明显优势 |

**评估模板：**
```markdown
## Model Selection 评估

### 简单方案对比
| 方案 | 准确率 | 延迟 | 成本 | 结论 |
|------|--------|------|------|------|
| 规则引擎 | 85% | <10ms | $0 | 备选 |
| 小模型(7B) | 92% | 200ms | $0.001/次 | 选择 |
| 大模型(70B) | 95% | 1000ms | $0.01/次 | 过度 |

### 选择理由
[当前模型有明显优势的理由]
```

---

## D2: Data Quality

**检查问题：**
- 训练数据有标注？
- 数据分布与生产一致？
- 边界case有覆盖？
- 数据偏见评估过？

**评估标准：**

| 状态 | 说明 |
|------|------|
| Ready | 数据质量明确，有测试集 |
| Risk | 数据质量不确定 |
| Blocker | 用了脏数据，没有验证 |

**评估模板：**
```markdown
## Data Quality 评估

### 数据集统计
- 训练集: N条
- 验证集: N条
- 测试集: N条

### 质量检查
| 检查项 | 结果 |
|--------|------|
| 标注一致性 | ✅/❌ |
| 分布一致性 | ✅/❌ |
| 边界case覆盖 | ✅/❌ |
| 偏见评估 | ✅/❌ |

### 问题case示例
[列出已知的边界case和处理方式]
```

---

## D3: Cost Modeling

**检查问题：**
- 单次调用成本计算过？
- 规模化成本估算过？
- 预算边界在哪？
- 成本超支的应对？

**评估标准：**

| 状态 | 说明 |
|------|------|
| Ready | 成本模型建立，规模化可接受 |
| Risk | 成本估算不确定 |
| Blocker | 没有成本模型，不知道贵不贵 |

**成本计算模板：**
```markdown
## Cost Modeling

### 单次成本
| 组件 | 计算 | 成本 |
|------|------|------|
| LLM调用 | tokens × price | $0.001 |
| API调用 | 次 × price | $0.0001 |
| **单次总计** | | **$0.0011** |

### 规模化成本
| 规模 | 日调用 | 月成本 | 年成本 |
|------|--------|--------|--------|
| 100用户 | 1,000 | $33 | $396 |
| 1,000用户 | 10,000 | $330 | $3,960 |
| 10,000用户 | 100,000 | $3,300 | $39,600 |

### 成本优化策略
[列出可能的成本优化手段]
```

---

## D4: Production Monitoring

**检查问题：**
- 有请求量监控？
- 有延迟监控？
- 有错误率监控？
- 有业务指标监控？
- 告警阈值设定？

**评估标准：**

| 状态 | 说明 |
|------|------|
| Ready | 监控完善，有告警 |
| Risk | 部分监控 |
| Blocker | 无监控，不知道状态 |

**监控清单：**
```markdown
## Monitoring 清单

### 基础监控
- [ ] 请求量 (QPS)
- [ ] 响应延迟 (P50/P95/P99)
- [ ] 错误率
- [ ] 可用率

### 业务监控
- [ ] AI功能使用率
- [ ] 功能成功率
- [ ] 用户满意度

### 告警配置
- [ ] 延迟 > X ms 告警
- [ ] 错误率 > X% 告警
- [ ] 业务指标异常告警
```

---

## D5: Failure UX

**检查问题：**
- AI失败时的用户体验？
- 有fallback方案？
- 失败信息对用户友好？
- 用户知道AI失败了？

**评估标准：**

| 状态 | 说明 |
|------|------|
| Ready | 有明确failure UX，优雅降级 |
| Risk | 部分场景有处理 |
| Blocker | AI失败就是报错/无响应 |

**Failure UX模板：**
```markdown
## Failure UX

### 失败场景
| 场景 | 当前处理 | 改进方案 |
|------|----------|----------|
| 模型超时 | 显示"加载中..." | 添加重试+超时提示 |
| API限流 | 报错 | 队列+告知用户等待 |
| 输入无效 | 报错 | 友好的错误提示+修正建议 |
| 输出异常 | 显示原文 | 降级为规则+提示 |

### Fallback策略
1. [具体fallback方案]
2. [备选方案]
3. [最终兜底]
```

---

## D6: System Optimization

**检查问题：**
- 测了正确的指标？
- 有A/B测试能力？
- 有Canary发布能力？
- 性能瓶颈识别？

**评估标准：**

| 状态 | 说明 |
|------|------|
| Ready | 指标正确，有A/B测试 |
| Risk | 指标部分正确 |
| Blocker | 指标不正确，无法评估 |

**优化清单：**
```markdown
## Optimization 清单

### 指标设计
- [ ] 核心指标定义 (North Star Metric)
- [ ] 代理指标定义
- [ ] 指标可采集

### 发布能力
- [ ] A/B测试框架
- [ ] Canary发布
- [ ] 快速回滚

### 性能
- [ ] 延迟瓶颈识别
- [ ] 吞吐量测试
- [ ] 资源使用评估
```

---

## 综合报告模板

```markdown
# AI Health Check Report

## 功能: [功能名称]
## 日期: YYYY-MM-DD
## 检查人: [姓名]

## 总体判决: [Ready / Needs Work / Don't Ship]

---

### Ready: [维度列表]
### Risk: [维度列表]
### Blocker: [维度列表]

---

## 详细评估

### D1 Model Selection: [Ready/Risk/Blocker]
[评估详情]

### D2 Data Quality: [Ready/Risk/Blocker]
[评估详情]

### D3 Cost Modeling: [Ready/Risk/Blocker]
[评估详情]

### D4 Monitoring: [Ready/Risk/Blocker]
[评估详情]

### D5 Failure UX: [Ready/Risk/Blocker]
[评估详情]

### D6 Optimization: [Ready/Risk/Blocker]
[评估详情]

---

## 必须修复的问题

1. [Blocker问题1]
2. [Blocker问题2]

## 建议改进

1. [Risk问题1]
2. [Risk问题2]
```

## 检查清单

- [ ] D1: Model Selection评估完成
- [ ] D2: Data Quality评估完成
- [ ] D3: Cost Modeling评估完成
- [ ] D4: Monitoring评估完成
- [ ] D5: Failure UX评估完成
- [ ] D6: Optimization评估完成
- [ ] 总体判决明确
- [ ] 问题有负责人和截止日期

## 红牌警告

- 没有成本模型就上线AI功能
- AI失败就是报错给用户
- 无法监控AI功能是否正常
- 没有测试过简单方案就用大模型
- 数据质量没验证就上线

## 好/坏对比

**好：**
```
AI Health Check: Email Composer
总体判决: Needs Work (4/6 ready)

Ready: Model Selection, Monitoring, Optimization
Risk: Data Quality, Failure UX
Blocker: Cost Modeling

结论: 有Cost Blocker，修复前不能发布
```

**坏：**
```
AI功能上线了
没人算过成本
也不知道怎么监控
失败了用户就看到报错
（等出问题就被动了）
```
