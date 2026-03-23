---
name: engineering-code-review
description: Use when reviewing code changes, providing feedback, or conducting code review sessions.
---

# Code Review Skill

高效、专业的代码审查。

## 何时使用

- PR/代码审查
- 代码合并前检查
- 安全漏洞发现
- 代码质量提升
- 知识共享

## 代码审查流程

```
1. 准备审查 → 2. 执行审查 → 3. 反馈意见 → 4. 讨论确认 → 5. 合并批准
```

### 1. 准备审查

**提交信息规范：**

```markdown
## Commit Message规范

### Angular规范
```
<type>(<scope>): <subject>

<body>

<footer>
```

### Type类型
| 类型 | 说明 | 示例 |
|------|------|------|
| feat | 新功能 | feat(user): add login |
| fix | Bug修复 | fix(order): order not found |
| docs | 文档 | docs: update README |
| style | 格式 | style: format code |
| refactor | 重构 | refactor: simplify logic |
| test | 测试 | test: add unit tests |
| chore | 构建 | chore: update deps |

### 好/坏Commit
**好：**
```
feat(user): add password reset functionality

- Add reset_password endpoint
- Add email verification
- Add token generation
- Update user model

Closes #123
```

**坏：**
```
fix stuff
update code
asdf
```
```

**PR描述模板：**

```markdown
## PR描述模板

```markdown
## 概述
[简要描述这个PR做了什么]

## 改动
[详细列出改动内容]

### 新增
- [ ]

### 修改
- [ ]

### 删除
- [ ]

## 测试
- [ ] 单元测试通过
- [ ] 集成测试通过
- [ ] 手动测试完成

## 截图/日志
[如有UI改动或日志输出]

## 相关Issue
Closes #123
```
```

### 2. 执行审查

**审查维度：**

```markdown
## 审查维度

### 代码正确性
- [ ] 功能符合需求
- [ ] 边界条件处理
- [ ] 错误处理完善
- [ ] 单元测试覆盖

### 代码质量
- [ ] 命名规范
- [ ] 代码可读性
- [ ] 函数长度
- [ ] 重复代码

### 架构设计
- [ ] 模块解耦
- [ ] 扩展性
- [ ] 技术选型合理

### 安全性
- [ ] 输入验证
- [ ] SQL注入防护
- [ ] XSS防护
- [ ] 权限检查

### 性能
- [ ] 数据库索引
- [ ] 缓存使用
- [ ] 循环优化
- [ ] N+1查询
```

### 3. 反馈意见

**审查意见模板：**

```markdown
## 审查意见

### 必须修改 (Blocking)
```markdown
**[BLOCK]** 文件: src/user.py:45

问题：未处理空用户情况，会导致NPE

建议：
```python
# 当前代码
user = get_user(user_id)
return user.name

# 建议修改
user = get_user(user_id)
if not user:
    raise UserNotFoundError(user_id)
return user.name
```
```

### 建议优化 (Non-blocking)
```markdown
**[NIT]** 文件: src/order.py:78

问题：函数过长，可读性差

建议：拆分为多个小函数
- extract_order_items()
- calculate_discount()
- format_order_response()
```

### 点赞 (Praise)
```markdown
**[PRAISE]** 文件: src/payment.py:56

很好的错误处理设计，使用了自定义异常，
比直接返回错误码好得多！
```
```

### 4. 讨论确认

**审查原则：**

```markdown
## 审查原则

### 对事不对人
- ❌ "你这个代码写得很烂"
- ✅ "这个实现有问题，建议..."

### 具体可执行
- ❌ "这段代码需要优化"
- ✅ "这个循环可以并行化，建议使用multiprocessing"

### 关注价值
- ✅ 阻塞问题必须改
- ⚠️ 优化建议看情况
- 💡 好代码要表扬

### 促进学习
- 分享最佳实践
- 解释为什么
- 提供参考链接
```

## 代码审查检查清单

- [ ] Commit规范检查
- [ ] PR描述完整
- [ ] 功能正确性
- [ ] 代码质量
- [ ] 安全漏洞
- [ ] 性能问题
- [ [ ] 测试覆盖
- [ ] 文档更新
- [ ] 变更范围评估

## 红牌警告

- 功能逻辑错误
- 安全漏洞
- 严重性能问题
- 破坏性变更
- 缺少必要测试
- 无法合并冲突
- 审查意见不处理
