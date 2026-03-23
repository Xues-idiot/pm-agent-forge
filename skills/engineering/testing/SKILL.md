---
name: engineering-testing
description: Use when designing test strategies, writing unit tests, or managing quality assurance. Covers test pyramid, TDD, BDD, test coverage, and quality gates.
---

# Testing Strategy

测试策略与质量保障。

## 何时使用

- 测试策略设计
- 单元测试编写
- 集成测试
- 端到端测试
- 测试覆盖率分析

## 测试基础

### 测试金字塔

```markdown
## 测试金字塔

### 各层特点
| 层级 | 比例 | 特点 | 工具 |
|------|------|------|------|
| E2E | 10% | 真实场景 | Selenium/Cypress |
| Integration | 20% | 模块交互 | TestContainers |
| Unit | 70% | 快速隔离 | JUnit/Pytest |

### 投入产出
```markdown
## 测试投入

### 单元测试
- 成本：低（写代码时）
- 收益：高（快速反馈）
- 覆盖：核心逻辑

### 集成测试
- 成本：中（环境准备）
- 收益：中（交互验证）
- 覆盖：接口协议

### E2E测试
- 成本：高（维护难）
- 收益：高（真实验证）
- 覆盖：关键路径
```

### 测试原则
| 原则 | 说明 | 实践 |
|------|------|------|
| FIRST | 快速/独立/可重复 | 测试规范 |
| 右侧内容 | 测试替身 | Mock/Stub |
| Arrange-Act-Assert | 结构化 | AAA模式 |
```

## 单元测试

### 测试结构

```markdown
## 单元测试结构

### AAA模式
```python
## AAA模式示例

# Arrange - 准备
user_repo = Mock(UserRepository)
user_service = UserService(user_repo)

# Act - 执行
result = user_service.get_user(1)

# Assert - 断言
assert result.name == "test"
```

### 测试命名
| 命名 | 格式 | 示例 |
|------|------|------|
| 方法 | test_方法_场景 | test_create_user_success |
| 行为 | should_行为_when | should_return_null_when_not_found |
| 场景 | given_when_then | given_valid_input_when_create |
```

### 断言技巧

```markdown
## 断言实践

### 常用断言
| 断言 | 适用 | 工具 |
|------|------|------|
| 相等 | 值验证 | assertEqual |
| 异常 | 错误处理 | assertRaises |
| 布尔 | 状态验证 | assertTrue |
| 范围 | 数值验证 | assertGreater |

### 好的断言
```python
## 好的断言

# ❌ 不好 - 断言消息不清晰
assert result == expected

# ✅ 好 - 清晰的错误消息
assert result == expected, f"Expected {expected}, got {result}"

# ✅ 好 - 语义化
assert_user_created_with_correct_fields(result, expected_name, expected_email)
```
```

## TDD开发

### TDD流程

```markdown
## TDD循环

### 红绿重构
```markdown
## TDD步骤

1. Red - 写一个失败的测试
   - 明确需求
   - 快速实现

2. Green - 让测试通过
   - 最简单方式
   - 不考虑优化

3. Refactor - 重构
   - 消除重复
   - 提升质量
```

### TDD优势
| 优势 | 说明 |
|------|------|
| 设计驱动 | 测试先行 |
| 快速反馈 | 增量验证 |
| 文档化 | 测试即文档 |
| 重构自信 | 回归保护 |
```

## 集成测试

### 测试策略

```markdown
## 集成测试

### 测试范围
| 范围 | 说明 | 示例 |
|------|------|------|
| 数据库 | 数据层 | CRUD |
| 文件系统 | 文件操作 | 上传/读取 |
| 外部服务 | API调用 | 第三方 |
| 消息队列 | 异步消息 | 发送/消费 |

### 测试数据库
| 方案 | 特点 | 适用 |
|------|------|------|
| H2内存 | 快速/隔离 | 开发 |
| TestContainers | 真实数据库 | CI环境 |
| 真实数据库 | 最真实 | 集成环境 |
```

### Mock策略
```python
## Mock使用

# ✅ 正确使用Mock
user_repo = Mock(spec=UserRepository)
user_repo.get_by_id.return_value = User(id=1, name="test")

# ❌ 滥用Mock
user_repo = Mock()
user_repo.get_by_id.return_value = "fake data"

# 原则：Mock接口而非实现
```

## 端到端测试

### E2E框架

```markdown
## E2E测试框架

### 框架对比
| 框架 | 语言 | 特点 | 适用 |
|------|------|------|------|
| Selenium | 多语言 | 成熟 | Web |
| Cypress | JS | 现代化 | Web |
| Playwright | 多语言 | 跨平台 | Web/API |
| Appium | 多语言 | 移动端 | App |

### 测试策略
```markdown
## E2E策略

### 关键路径
- 登录/注册
- 核心功能
- 支付流程
- 异常场景

### 避免
- 全流程覆盖
- 频繁执行
- 复杂断言
```

## 测试覆盖率

### 覆盖率指标

```markdown
## 覆盖率分析

### 指标类型
| 类型 | 说明 | 目标 |
|------|------|------|
| 行覆盖率 | 代码行执行 | >80% |
| 分支覆盖率 | 条件分支 | >70% |
| 函数覆盖率 | 函数调用 | >90% |
| 路径覆盖率 | 执行路径 | 关键路径 |

### 覆盖率陷阱
```markdown
## 不要盲目追求覆盖率

### ❌ 错误做法
- 100%覆盖率目标
- 测试无价值的代码
- Mock一切

### ✅ 正确做法
- 核心逻辑优先
- 边界条件覆盖
- 真实依赖测试
```

## 质量门禁

### CI集成

```markdown
## 质量门禁

### 门禁检查
| 检查 | 阈值 | 工具 |
|------|------|------|
| 单元测试 | >80% | JaCoCo |
| 代码规范 | 0违规 | ESLint |
| 安全扫描 | 0高危 | SonarQube |
| 依赖检查 | 无漏洞 | Snyk |

### 质量门禁流程
```markdown
## 门禁流程

1. 代码提交
2. 自动触发CI
3. 执行质量检查
4. 检查是否通过
5. 通过后合并
6. 失败则阻止
```
```

## 检查清单

- [ ] 测试策略清晰
- [ ] 单元测试覆盖核心逻辑
- [ ] 集成测试覆盖接口
- [ ] E2E测试覆盖关键路径
- [ ] 测试可独立运行
- [ ] 覆盖率达标
- [ ] 质量门禁完善

## 红牌警告

- 无测试策略
- 测试覆盖率低
- 测试不稳定（Flaky）
- 单元测试依赖外部
- Mock滥用
- 忽略失败的测试
- 测试无维护
