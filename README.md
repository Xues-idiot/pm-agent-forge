# PM-Agent-Forge

> 帮助 Coding Agent 更好地开发 PM Agent 和私域运营 Agent 的框架

## 核心理念

Pi (PM智能助理) 和 Nu (私域运营工具) 是特殊的 Agent，不是写代码的 Coding Agent，而是处理业务任务的 Agent。

PM-Agent-Forge 提供了：
- **Skills**: PM/私域运营专业技能
- **Subagents**: 任务专用子代理
- **Workflows**: 开发流程规范
- **Reviewers**: 领域专家审核

## 三大核心机制（融合三个参考项目）

### 1. Skills 系统（来自 Superpowers + Everything Claude Code）

Skills 是触发式的专业技能模块，自动基于上下文激活：

```
skills/
├── pm/
│   ├── prd-writing/          # PRD 最佳实践
│   ├── user-research/         # 用户调研方法
│   ├── competitive-analysis/   # 竞品分析
│   └── market-insight/        # 市场洞察
├── private-ops/
│   ├── campaign-design/       # 营销活动设计
│   ├── rfm-analysis/          # RFM 用户分层
│   ├── content-strategy/      # 内容策略
│   └──转化优化/              # 转化率优化
└── meta/
    ├── agent-evolution/       # Agent 自我进化
    └── quality-verification/   # 质量验证
```

### 2. Subagent Templates（来自 Deep Agents + Everything Claude Code）

针对不同任务的专用子代理：

```
agents/
├── research-agent.md          # 信息调研
├── prd-writer-agent.md        # PRD 写作
├── campaign-designer-agent.md  # 营销活动设计
├── analytics-agent.md          # 数据分析
└── qa-agent.md               # 质量保证
```

### 3. Development Workflow（来自 Superpowers）

```
1. brainstorming    → 需求澄清（与用户确认）
2. planning        → 制定实施计划
3. researching     → 调研相关信息
4. implementing    → 实现功能
5. reviewing       → 两阶段审核（规格 + 质量）
6. evolving        → 自我进化检查
```

## 核心 Skills

### PM PRD Writing Skill
```yaml
name: pm-prd-writing
description: Use when writing or reviewing PRD documents
trigger: prd, product requirements, specification
```

### Agent Evolution Skill
```yaml
name: agent-evolution
description: Use when Pi/Nu needs to self-improve
trigger: evolve, improve, iterate, learn
```

## 使用方法

在 Claude Code 项目中添加：
```bash
# 安装 PM-Agent-Forge
/plugin install pm-agent-forge@your-marketplace
```

或手动复制 `skills/` 和 `agents/` 到项目。

## 项目结构

```
pm-agent-forge/
├── skills/              # Skills 技能库
│   ├── pm/             # PM 相关技能
│   ├── private-ops/     # 私域运营技能
│   └── meta/           # 元技能
├── agents/             # Subagent 模板
├── workflows/          # 工作流程定义
├── templates/         # 文档模板
└── docs/              # 文档
```

## License

MIT
