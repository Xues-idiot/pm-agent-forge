---
name: engineering-test-strategy
description: Use when designing test strategies, planning test coverage, or creating testing frameworks.
---

# Test Strategy Skill

设计全面、有效的测试策略。

## 何时使用

- 测试策略制定
- 测试覆盖率规划
- 测试框架选型
- 测试自动化设计
- 测试流程优化

## 测试策略流程

```
1. 需求分析 → 2. 测试设计 → 3. 框架选型 → 4. 自动化实施 → 5. 持续集成
```

### 1. 需求分析

**测试分层模型：**

```markdown
## 测试金字塔

        ┌─────────────┐
        │   E2E测试   │     少量、关键路径
        ├─────────────┤
        │  集成测试   │     按模块边界
        ├─────────────┤
        │   单元测试   │     大量、快速
        └─────────────┘

### 各层比例建议
| 层级 | 占比 | 执行频率 |
|------|------|---------|
| 单元测试 | 70% | 每次提交 |
| 集成测试 | 20% | 每日构建 |
| E2E测试 | 10% | 部署前 |
```

**测试类型：**

```markdown
## 测试类型

| 类型 | 目标 | 工具 |
|------|------|------|
| 单元测试 | 函数/方法 | pytest, JUnit |
| 集成测试 | 模块交互 | pytest, TestNG |
| E2E测试 | 完整流程 | Selenium, Playwright |
| 性能测试 | 负载/压力 | k6, JMeter |
| 安全测试 | 漏洞扫描 | OWASP ZAP |
| 契约测试 | API协议 | Pact |
```

### 2. 测试设计

**测试用例设计：**

```markdown
## 测试用例设计

### 等价类划分
```python
# 输入：用户名（6-18位字母数字）
class TestUsername:
    def test_valid_username(self):
        assert validate_username("user123") is True

    def test_too_short(self):
        assert validate_username("user") is False

    def test_too_long(self):
        assert validate_username("a" * 19) is False

    def test_special_chars_invalid(self):
        assert validate_username("user@123") is False
```

### 边界值分析
```python
# 边界值测试
def test_boundary_values():
    # 最小有效值
    assert validate_username("u" * 6) is True
    # 最大有效值
    assert validate_username("u" * 18) is True
    # 刚好低于最小
    assert validate_username("u" * 5) is False
    # 刚好高于最大
    assert validate_username("u" * 19) is False
```

### 场景测试
```python
def test_user_registration_flow():
    """完整的用户注册流程"""
    # 1. 创建用户
    user = create_user("test@example.com")
    assert user.status == "pending"

    # 2. 验证邮箱
    verify_email(user.id, "token123")
    user.reload()
    assert user.status == "active"

    # 3. 登录
    token = login("test@example.com", "password123")
    assert token is not None
```

### 异常测试
```python
def test_duplicate_email_error():
    """邮箱重复注册"""
    create_user("test@example.com")
    with pytest.raises(DuplicateEmailError):
        create_user("test@example.com")

def test_invalid_email_format():
    """无效邮箱格式"""
    with pytest.raises(InvalidEmailError):
        create_user("not-an-email")
```
```

### 3. 框架选型

**框架对比：**

```markdown
## 测试框架选型

### Python
| 框架 | 适用场景 | 特点 |
|------|---------|------|
| pytest | 通用 | 简单、功能强 |
| unittest | 标准库 | 无需安装 |
| pytest-django | Django | Django集成 |

### JavaScript/TypeScript
| 框架 | 适用场景 | 特点 |
|------|---------|------|
| Jest | React/Vue | 零配置 |
| Vitest | 现代框架 | 快、轻 |
| Mocha | 通用 | 灵活 |

### Java/Kotlin
| 框架 | 适用场景 | 特点 |
|------|---------|------|
| JUnit 5 | 标准 | 事实标准 |
| TestNG | 复杂测试 | 依赖管理 |

### Go
| 框架 | 适用场景 | 特点 |
|------|---------|------|
| testing | 标准库 | 简单 |
| testify | 高级断言 | 丰富 |
```

### 4. 自动化实施

**Pytest最佳实践：**

```python
## Pytest结构

# tests/test_user.py

import pytest
from app.models import User

@pytest.fixture
def user_data():
    """共享的测试数据fixture"""
    return {
        "name": "Test User",
        "email": "test@example.com",
        "password": "password123"
    }

@pytest.fixture
def created_user(user_data):
    """创建并清理测试用户"""
    user = User.create(**user_data)
    yield user
    user.delete()

class TestUserModel:
    """用户模型测试"""

    def test_create_user(self, user_data):
        user = User.create(**user_data)
        assert user.id is not None
        assert user.email == user_data["email"]

    def test_user_not_found(self):
        with pytest.raises(UserNotFoundError):
            User.get_by_id(99999)

    def test_duplicate_email(self, user_data):
        User.create(**user_data)
        with pytest.raises(DuplicateEmailError):
            User.create(**user_data)

class TestUserAuthentication:
    """用户认证测试"""

    def test_login_success(self, created_user):
        token = authenticate(
            created_user.email,
            "password123"
        )
        assert token is not None

    def test_login_wrong_password(self, created_user):
        with pytest.raises(InvalidPasswordError):
            authenticate(created_user.email, "wrong")
```

**Mock使用：**

```python
## Mock示例

from unittest.mock import Mock, patch

def test_payment_failure():
    """支付失败处理"""
    with patch('app.services.payment.PaymentGateway') as mock_gateway:
        mock_gateway.charge.return_value = {
            "status": "failed",
            "error": "insufficient_funds"
        }

        with pytest.raises(PaymentFailedError):
            process_payment(order_id=123, amount=100)
```

### 5. 持续集成

**CI配置：**

```yaml
## GitHub Actions示例

name: Test

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'

      - name: Install dependencies
        run: |
          pip install pytest pytest-cov
          pip install -r requirements.txt

      - name: Run tests
        run: |
          pytest tests/ \
            --cov=app \
            --cov-report=xml \
            --cov-fail-under=80

      - name: Upload coverage
        uses: codecov/codecov-action@v3
```

## 测试策略检查清单

- [ ] 测试分层合理
- [ ] 覆盖率达标
- [ ] 用例设计完整
- [ ] 框架选型合适
- [ ] Mock使用恰当
- [ ] CI配置正确
- [ ] 测试独立运行
- [ ] 定期清理无效测试

## 红牌警告

- 测试覆盖率低于目标
- 测试执行时间过长
- 测试相互依赖
- 测试结果不稳定
- Mock使用过度
- 缺少边界测试
- 忽略异常场景
- 测试文档缺失
