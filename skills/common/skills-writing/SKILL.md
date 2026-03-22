---
name: common-skills-writing
description: Use when creating new Skills, improving existing Skills, or learning how to structure Skill documentation. Activates when building the Skills library.
---

# Skills Writing Skill

如何编写高质量的 Skill 文档。本技能参考 Superpowers 的写作规范。

## 何时使用

- 创建新的 Skill
- 改进现有的 Skill
- 学习 Skill 写作规范
- 审核他人写的 Skill

## Skill 结构

### YAML Frontmatter（必需）

每个 Skill 必须以 YAML frontmatter 开头：

```yaml
---
name: skill-name-with-hyphens
description: Use when [triggering conditions and situations]
---
```

**命名规则：**
- 只能包含字母、数字、中划线
- 不允许：括号、特殊字符、下划线
- 格式：`领域-技能名称`

**Description 规则：**
- 以 "Use when..." 开头
- 描述触发条件，不是技能功能
- 第三人称视角
- 最大 1024 字符

### 章节结构（推荐）

**标准章节顺序：**

| 章节 | 必要性 | 说明 |
|------|-------|------|
| Overview | 推荐 | 1-2 句话说明核心原则 |
| 何时使用 | 必需 | 明确触发场景 |
| 流程/方法 | 推荐 | 具体执行步骤 |
| 模板 | 可选 | 输出模板 |
| 检查清单 | 推荐 | 完成后自检 |
| 红牌警告 | 推荐 | 停止信号 |

## 写作原则

### 清晰性原则

**好例子：**
```markdown
## 何时使用
- 用户说"帮我写个 PRD"
- 收到"product requirements"相关上下文
- 需要评审产品规格文档
```

**坏例子：**
```markdown
## 何时使用
- 需要写文档的时候
- 涉及产品相关的内容
```

### 具体性原则

**好例子：**
```markdown
## 步骤
1. 确认用户类型（产品经理/开发/运营）
2. 收集需求（功能、目标、限制）
3. 验证需求（是否有模糊点）
```

**坏例子：**
```markdown
## 步骤
1. 了解需求
2. 写文档
3. 完成
```

### 可执行性原则

**好例子：**
```markdown
## PRD 模板
# PRD: [产品名] - [功能名]

## 1. 概述
- 背景：[具体背景]
- 目标：[SMART 目标]
- 成功指标：[可量化指标]
```

**坏例子：**
```markdown
## PRD 模板
# PRD

写清楚产品需求。
```

## Skill 模板

```markdown
---
name: [skill-name]
description: Use when [触发条件]
---

# [Skill 名称]

[Overview - 1-2 句话核心原则]

## 何时使用

[明确触发场景：]
- 场景1
- 场景2
- 何时不使用

## 流程

### 步骤1：[名称]
[具体操作]

### 步骤2：[名称]
[具体操作]

## 模板

### 模板1
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

## 常用结构元素

### 表格

```markdown
| 列1 | 列2 | 列3 |
|------|------|------|
| 内容 | 内容 | 内容 |
```

### 列表

```markdown
**步骤1**：[名称]
- 要点1
- 要点2

**步骤2**：[名称]
```

### 好/坏对比

```markdown
**好例子：**
```
[好的示例]
```

**坏例子：**
```
[坏的示例]
```
```

### 流程图（文字版）

```markdown
```
步骤1 → 步骤2 → 步骤3
              ↓
           步骤4
```
```

## 红牌警告写法

红牌警告告诉 Coding Agent 什么时候应该停止：

```markdown
## 红牌警告

- 信息来源单一
- 数据无法验证
- 与调研目标不相关
```

## 质量标准

| 标准 | 要求 |
|------|------|
| **完整性** | 覆盖主要场景 |
| **准确性** | 流程步骤正确 |
| **可执行性** | Agent 能执行 |
| **可维护性** | 易于更新 |

## 常见错误

| 错误 | 问题 | 修正 |
|------|------|------|
| 描述太长 | 超过 1024 字符 | 精简到触发条件 |
| 流程模糊 | "了解需求" | 具体化到"收集功能列表" |
| 缺少模板 | 只有文字描述 | 添加可复制模板 |
| 红牌警告空洞 | "注意质量" | 列出具体停止信号 |

## 跨 Skill 引用

引用其他 Skill 时使用：
```markdown
**REQUIRED SUB-SKILL:** Use [skill-name]
```

不要使用 `@skills/path/file.md`，这样会强制加载浪费 token。

## 写作检查清单

- [ ] name 符合命名规范
- [ ] description 以 "Use when" 开头
- [ ] description 不超过 1024 字符
- [ ] 包含"何时使用"章节
- [ ] 包含具体执行步骤
- [ ] 包含模板或示例
- [ ] 包含检查清单
- [ ] 包含红牌警告
- [ ] 内容具体可执行

## 进阶技巧

### 渐进式披露

Skill 可以设计为渐进式：
1. Frontmatter 只包含 name 和 description（始终加载）
2. Full content 按需加载

### 模块化

复杂 Skill 可拆分为：
```
skill/
├── SKILL.md          # 主 Skill
├── templates/        # 模板目录
│   ├── template1.md
│   └── template2.md
└── examples/        # 示例目录
    ├── good.md
    └── bad.md
```

### 持续改进

根据使用反馈优化：
- 收集 Agent 执行中的问题
- 更新不清晰的步骤
- 添加遗漏的场景
