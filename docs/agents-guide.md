# Agents 指南

> 了解 13 个专业 Agent 的职责和使用场景

---

## Agent 概览

| Agent | 模型 | 用途 |
|-------|------|------|
| research-agent | Opus | 信息调研 |
| prd-writer-agent | Opus | PRD 写作 |
| campaign-designer-agent | Opus | 营销活动设计 |
| analytics-agent | Sonnet | 数据分析 |
| qa-agent | Sonnet | 质量保证 |
| customer-service-agent | Sonnet | 客服支持 |
| data-analytics-agent | Sonnet | 数据分析 |
| education-agent | Sonnet | 教育培训 |
| finance-agent | Sonnet | 金融分析 |
| hr-agent | Sonnet | 人力资源 |
| iot-agent | Sonnet | 物联网 |
| medical-agent | Sonnet | 医疗辅助 |
| legal-agent | Sonnet | 法律服务 |

---

## 详细说明

### research-agent (Opus)

**用途**：信息调研

**触发场景**：
- 市场调研
- 竞品分析
- 行业研究
- 数据收集

**执行流程**：
1. 明确调研目标
2. 收集信息源
3. 分析整理
4. 输出报告

---

### prd-writer-agent (Opus)

**用途**：PRD 写作

**触发场景**：
- 写新产品 PRD
- 更新现有 PRD
- 评审产品规格

**执行流程**：
1. 需求理解
2. 用户分析
3. 功能设计
4. 输出 PRD

---

### campaign-designer-agent (Opus)

**用途**：营销活动设计

**触发场景**：
- 设计营销活动
- 策划用户激活
- 制定推广策略

**执行流程**：
1. 明确活动目标
2. 分析目标用户
3. 设计活动机制
4. 制定触达计划
5. 预估效果
6. 复盘优化

---

### analytics-agent (Sonnet)

**用途**：数据分析

**触发场景**：
- 数据趋势分析
- 业务数据分析
- 用户行为分析

**相关 Skills**：
- data-processing
- visualization-creation
- metric-calculation

---

### qa-agent (Sonnet)

**用途**：质量保证

**触发场景**：
- 代码评审
- 测试用例设计
- 质量评估

---

### customer-service-agent (Sonnet)

**用途**：客服支持

**触发场景**：
- 处理客户咨询
- 解答常见问题
- 投诉处理

**相关 Skills**：
- faq-handling
- ticket-routing
- complaint-handling

---

### data-analytics-agent (Sonnet)

**用途**：数据分析和BI

**触发场景**：
- 数据报表生成
- Dashboard 设计
- 数据治理

**相关 Skills**：
- report-generation
- dashboard-design
- data-governance

---

### education-agent (Sonnet)

**用途**：教育培训

**触发场景**：
- 课程设计
- 学习评估
- 学员管理

**相关 Skills**：
- course-design
- learning-assessment
- student-retention

---

### finance-agent (Sonnet)

**用途**：金融分析

**触发场景**：
- 风险评估
- 投资分析
- 财务报告分析

**相关 Skills**：
- risk-assessment
- investment-analysis
- financial-report-analysis

---

### hr-agent (Sonnet)

**用途**：人力资源

**触发场景**：
- 招聘管理
- 绩效评估
- 员工培训

**相关 Skills**：
- resume-screening
- performance-evaluation
- employee-training

---

### iot-agent (Sonnet)

**用途**：物联网

**触发场景**：
- 设备管理
- 监控告警
- 预测性维护

**相关 Skills**：
- device-management
- monitoring-alerting
- predictive-maintenance

---

### medical-agent (Sonnet)

**用途**：医疗辅助

**触发场景**：
- 病历分析
- 诊断辅助
- 健康管理

**相关 Skills**：
- medical-record-analysis
- diagnostic-assistance
- health-management

---

### legal-agent (Sonnet)

**用途**：法律服务

**触发场景**：
- 合同审查
- 法律研究
- 合规检查

**相关 Skills**：
- contract-review
- legal-research
- compliance-check

---

## 如何选择 Agent

```
任务类型 → 首选 Agent → 备选

写PRD → prd-writer-agent → research-agent
做调研 → research-agent → analytics-agent
设计活动 → campaign-designer-agent →
数据分析 → analytics-agent / data-analytics-agent
客服 → customer-service-agent →
HR → hr-agent →
金融 → finance-agent →
法律 → legal-agent →
医疗 → medical-agent →
IoT → iot-agent →
教育 → education-agent →
```

---

## Agent 文件格式

```markdown
---
name: agent-name
description: Expert [role] for [tasks]. Use when [triggering conditions].
model: [opus/sonnet]
tools: ["Read", "Write", "Grep"]
---

# Agent Name

[角色描述]

## 你的角色
- 角色1
- 角色2

## 执行流程
1. 步骤1
2. 步骤2
3. 步骤3

## 场景示例

### 场景1
[描述]

## 红牌警告
- 警告1
- 警告2
```

---

*参考：agents/ 目录下的各个 agent 文件*
