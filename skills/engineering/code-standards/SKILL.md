---
name: engineering-code-standards
description: Use when establishing coding conventions, writing clean code, or implementing code style guidelines.
---

# Code Standards Skill

编写规范、可读、易维护的代码。

## 何时使用

- 制定代码规范
- 代码审查
- 重构老代码
- 新项目初始化
- 团队规范统一

## 代码规范流程

```
1. 规范制定 → 2. 工具集成 → 3. 实践落地 → 4. 持续改进
```

### 1. 规范制定

**命名规范：**

```markdown
## 命名规范

### 变量命名
| 类型 | 风格 | 示例 |
|------|------|------|
| 变量 | 小写下划线/camelCase | user_name, userName |
| 常量 | 全大写下划线 | MAX_RETRY, API_KEY |
| 布尔 | is/has/can前缀 | is_active, has_permission |

### 函数命名
| 类型 | 风格 | 示例 |
|------|------|------|
| 函数 | 动词+名词 | get_user, create_order |
| 布尔函数 | is/has/can | is_valid, has_access |

### 类命名
| 类型 | 风格 | 示例 |
|------|------|------|
| 类 | 大写驼峰 | UserService, OrderController |
| 接口 | 大写驼峰+I前缀 | IUserService |
```

**代码结构规范：**

```markdown
## 代码结构

### 函数设计原则
- 单一职责：每个函数只做一件事
- 短小精悍：建议不超过30行
- 参数控制：参数不超过3个

### 错误处理
```python
# 好例子
try:
    result = process_data(data)
except ValidationError as e:
    logger.warning(f"Validation failed: {e}")
    raise BusinessError(f"Invalid data: {e}")
except Exception as e:
    logger.error(f"Unexpected error: {e}")
    raise

# 坏例子
try:
    result = process_data(data)
except:
    pass
```

### 注释规范
```python
# 单行注释：解释"为什么"而不是"是什么"

def calculate_discount(user):
    """计算用户折扣。

    Args:
        user: 用户对象

    Returns:
        折扣比例 (0-1)

    Raises:
        InvalidUserError: 用户无效
    """
    if not user.is_active:
        raise InvalidUserError("Inactive user")
    return user.loyalty_points * 0.01
```
```

### 2. 工具集成

**Linting配置：**

```markdown
## Lint工具配置

### ESLint (JavaScript)
```json
{
  "extends": ["airbnb", "prettier"],
  "rules": {
    "no-unused-vars": "error",
    "prefer-const": "error",
    "max-len": ["error", 100]
  }
}
```

### Pylint (Python)
```ini
[MESSAGES CONTROL]
disable=C0111,C0103,R0903

[FORMAT]
max-line-length=100
indent-string='    '
```

### Rustfmt (Rust)
```toml
max_width = 100
edition = "2021"
```

### Prettier (通用格式化)
```json
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5"
}
```
```

### 3. 实践落地

**Clean Code原则：**

```markdown
## Clean Code实践

### 好代码 vs 坏代码

**坏代码：**
```python
def process(d):
    if d:
        if d['type'] == 'user':
            if 'data' in d:
                return d['data'][0]['name']
    return None
```

**好代码：**
```python
def get_first_username(data):
    """获取第一个用户名。

    Args:
        data: 包含用户数据的字典

    Returns:
        用户名，如果不存在返回None
    """
    if not is_valid_user_data(data):
        return None

    users = extract_users(data)
    return users[0].name if users else None
```

### 函数设计
```python
# 好的函数
def create_user(name: str, email: str) -> User:
    """创建新用户。"""
    validate_email(email)
    user = User(name=name, email=email)
    return user_repository.save(user)

# 避免：参数过多
def create_user(name, email, age, phone, address, city, country, zipcode):
    pass

# 解决：使用配置对象
def create_user(name: str, email: str, profile: UserProfile):
    pass
```

### 错误处理
```python
# 分层异常处理
class ServiceError(Exception):
    """业务异常基类"""
    pass

class UserNotFoundError(ServiceError):
    """用户不存在"""
    pass

class InvalidInputError(ServiceError):
    """输入无效"""
    pass

# 统一错误码
class ErrorCode:
    USER_NOT_FOUND = ("U001", "用户不存在")
    INVALID_INPUT = ("U002", "输入参数无效")
    PERMISSION_DENIED = ("P001", "权限不足")
```
```

### 4. 持续改进

**Code Review指南：**

```markdown
## Code Review检查点

### 规范检查
- [ ] 命名规范遵循
- [ ] 代码格式统一
- [ ] 注释完整必要

### 设计检查
- [ ] 函数职责单一
- [ ] 模块解耦
- [ ] 扩展性考虑

### 质量检查
- [ ] 错误处理
- [ ] 边界情况
- [ ] 性能影响
- [ ] 安全性

### 测试检查
- [ ] 有单元测试
- [ ] 测试覆盖核心逻辑
- [ ] 测试可维护
```

## 代码规范检查清单

- [ ] 命名规范统一
- [ ] 代码格式一致
- [ ] 注释清晰必要
- [ ] 函数短小
- [ ] 错误处理规范
- [ ] 测试覆盖
- [ ] 无硬编码
- [ ] 安全漏洞

## 红牌警告

- 代码难以阅读
- 函数过长
- 重复代码
- 硬编码
- 隐藏bug（空catch、return None）
- 安全漏洞（SQL注入、XSS）
- 性能问题（N+1查询、循环内IO）
