# Sigma 快速开始指南

> 5分钟了解 Sigma (PM-Agent-Forge) 框架

---

## Sigma 是什么？

Sigma 是一个帮助 **Coding Agent** 更好地开发 **PM Agent** 和 **私域运营 Agent** 的框架。

**核心理念**：Coding Agent 很强大，但缺乏结构化的开发方法和专业领域知识。Sigma 提供 Skills、Agents、Workflows，让 Coding Agent 开发 AI Agent 时有章可循。

---

## 核心机制

### 1. Skills（技能）⭐ 最重要

Skills 是触发式的专业技能模块，自动基于上下文激活。

**结构**：
```yaml
---
name: pm-prd-writing
description: Use when writing or reviewing PRD documents
---
```

**每个 Skill 包含**：
- 何时使用（触发条件）
- 具体执行流程
- 模板和示例
- 检查清单
- 红牌警告（HARD-GATE）

**使用方式**：
当 Coding Agent 遇到相关上下文时，会自动触发对应的 Skill：
- PRD 相关 → 触发 `pm-prd-writing`
- 用户调研 → 触发 `pm-user-research`
- 竞品分析 → 触发 `pm-competitive-analysis`

---

### 2. Agents（子代理）

针对不同任务的专用子代理，共 **13 个**：

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

---

### 3. Workflows（工作流）

标准化流程：`brainstorming → planning → executing → reviewing → evolving`

| Workflow | 用途 |
|----------|------|
| brainstorming | 头脑风暴 |
| planning | 制定计划 |
| executing | 执行任务 |
| reviewing | 评审复盘 |
| evolving | 持续进化 |

---

## Skills 领域覆盖

共 **75 个 Skills**，覆盖 **12 个领域**：

| 领域 | Skills数 | 代表技能 |
|------|----------|---------|
| PM | 17 | PRD写作、用户研究、竞品分析、埋点设计 |
| 私域运营 | 12 | 活动策划、会员体系、裂变活动、变现 |
| 客服 | 11 | FAQ处理、工单分配、投诉处理、主动服务 |
| 数据分析 | 9 | 数据清洗、可视化、用户画像、数据管道 |
| HR | 10 | 简历筛选、绩效评估、人才盘点、离职管理 |
| 金融 | 8 | 风险评估、投资分析、预算管理、税务筹划 |
| IoT | 8 | 设备管理、监控告警、预测性维护、安全 |
| 医疗 | 7 | 病历分析、诊断辅助、健康管理、远程医疗 |
| 法律 | 7 | 合同审查、知识产权、劳动争议、合规检查 |
| 教育 | 7 | 课程设计、学习评估、学员留存、证书管理 |
| Meta | 2 | Agent进化、质量验证 |
| Common | 1 | Skills写作 |

---

## 快速使用

### 安装

```bash
# 克隆仓库
git clone https://github.com/Xues-idiot/pm-agent-forge.git

# 或作为 submodule
git submodule add https://github.com/Xues-idiot/pm-agent-forge.git
```

### 在项目中使用

```bash
# 复制 skills 到项目
cp -r pm-agent-forge/skills <your-project>/skills

# 复制 agents 到项目
cp -r pm-agent-forge/agents <your-project>/agents
```

### 触发 Skills

Coding Agent 会根据上下文自动触发对应的 Skill。

也可以手动调用：
```
Use pm-prd-writing when writing PRD documents
```

---

## 贡献新 Skill

### 1. 创建目录

```bash
# 在对应领域下创建目录
mkdir skills/pm/new-skill
```

### 2. 创建 SKILL.md

```markdown
---
name: pm-new-skill
description: Use when [触发条件]
---

# New Skill

[概述 - 1-2句话核心原则]

## 何时使用

- 场景1
- 场景2

## 流程

### 步骤1：[名称]
[具体操作]

## 模板

```markdown
[模板内容]
```

## 检查清单

- [ ] 检查项1
- [ ] 检查项2

## 红牌警告

出现以下情况立即停止：
- 警告1
- 警告2
```

### 3. 更新 README.md

在对应领域的 Skills 表格中添加新技能。

---

## 质量标准

参考 Superpowers 的写作规范：

| 要素 | 要求 |
|------|------|
| **结构清晰** | Overview / 何时使用 / 流程 / 模板 / 检查清单 / 红牌警告 |
| **具体可执行** | 步骤明确，模板可复制 |
| **好/坏对比** | 展示正确和错误示例 |
| **红牌警告** | 告诉什么时候该停止 |

---

## 下一步

- 📖 阅读 [README.md](../README.md) 了解完整项目
- 📋 查看 [Skills 列表](../README.md#skills-系统)
- 🔧 查看 [Agents 定义](../agents/)
- 📝 查看 [PRD 模板](../templates/prd-template.md)
- 🔄 了解 [Evolution Loop](../_EVOLUTION-LOOP.md)

---

## 常见问题

**Q: Skills 和 Agents 有什么区别？**

A: Skills 是专业技能模块，按需触发；Agents 是完整的子代理，有角色定义和执行流程。

**Q: 如何选择使用哪个 Agent？**

A: 根据任务类型选择：
- 写 PRD → prd-writer-agent
- 做数据分析 → analytics-agent / data-analytics-agent
- 设计营销活动 → campaign-designer-agent

**Q: 如何扩展新的 Skills？**

A: 参考 [skills-writing](../skills/common/skills-writing/SKILL.md) 技能的指导。

---

*最后更新：2026-03-23*
