---
name: engineering-coding-standards
description: Use when writing code, establishing team coding standards, or reviewing code for style compliance. Covers naming conventions, code organization, documentation, and language-specific best practices.
---

# Engineering Coding Standards

建立和维护团队代码规范，确保代码一致性、可读性和可维护性。

## 何时使用

- 编写新代码
- 制定团队代码规范
- 代码评审
- 建立项目模板
- 新人入职培训

## 代码规范框架

### 1. 命名规范

**通用原则：**
```
✓ 清晰 > 简短
✓ 业务含义 > 技术术语
✓ 英文命名（避免拼音）
```

**命名对照表：**

| 类型 | 规范 | 示例 |
|------|------|------|
| 变量 | 小写下划线 / 驼峰 | `user_name`, `userName` |
| 常量 | 全大写下划线 | `MAX_RETRY_COUNT`, `API_TIMEOUT` |
| 函数 | 动词前缀 | `get_user()`, `create_order()` |
| 类 | 大驼峰 | `UserService`, `OrderController` |
| 文件 | 小写下划线 | `user_service.py`, `order_controller.ts` |
| 数据库表 | 小写下划线复数 | `users`, `order_items` |
| API端点 | RESTful | `GET /users/{id}`, `POST /orders` |

**禁用名称：**
```markdown
❌ 禁用：tmp, temp, data, info, stuff, thing
❌ 禁用：a, b, c, x, y, z
❌ 禁用：拼音或中文
```

### 2. 代码组织

**Python 项目结构：**
```
project/
├── src/                    # 源代码
│   ├── __init__.py
│   ├── models/             # 数据模型
│   ├── services/           # 业务逻辑
│   ├── api/                # API层
│   └── utils/              # 工具函数
├── tests/                  # 测试
│   ├── unit/
│   └── integration/
├── docs/                   # 文档
├── config/                 # 配置
└── scripts/                # 脚本
```

**函数组织原则：**
```python
# ✓ 好的函数：单一职责
def calculate_order_total(order_id: str) -> Decimal:
    """计算订单总金额"""
    order = get_order(order_id)
    items = get_order_items(order_id)
    subtotal = sum(item.price * item.quantity for item in items)
    discount = apply_discount(order.customer_type, subtotal)
    return subtotal - discount

# ❌ 坏的函数：多功能混杂
def process_order(order_id):
    # 获取订单、计算价格、应用折扣、发送通知、更新库存...
```

### 3. 代码文档

**Docstring 规范：**
```python
def calculate_discount(customer_type: str, amount: Decimal) -> Decimal:
    """
    根据客户类型计算折扣金额。

    Args:
        customer_type: 客户类型 ('vip', 'regular', 'new')
        amount: 原始金额

    Returns:
        折扣后的金额

    Raises:
        ValueError: 当客户类型无效时

    Example:
        >>> calculate_discount('vip', Decimal('100'))
        Decimal('85')
    """
    discount_rates = {
        'vip': Decimal('0.15'),
        'regular': Decimal('0.05'),
        'new': Decimal('0.10'),
    }
    if customer_type not in discount_rates:
        raise ValueError(f"Invalid customer_type: {customer_type}")
    return amount * discount_rates[customer_type]
```

**README 模板：**
```markdown
# 项目名称

简短描述

## 快速开始

```bash
pip install -r requirements.txt
python main.py
```

## 项目结构

| 目录/文件 | 说明 |
|-----------|------|
| `src/` | 源代码 |
| `tests/` | 测试 |

## 配置

环境变量说明

## API文档

接口列表
```

### 4. Git 提交规范

**提交信息格式：**
```
<type>(<scope>): <subject>

<body>

<footer>
```

**Type 类型：**
| Type | 说明 | 示例 |
|------|------|------|
| feat | 新功能 | feat(user): add password reset |
| fix | Bug修复 | fix(order): correct tax calculation |
| docs | 文档 | docs: update README |
| style | 格式 | style: format code |
| refactor | 重构 | refactor(auth): simplify token logic |
| test | 测试 | test: add user service tests |
| chore | 杂项 | chore: update dependencies |

**提交示例：**
```bash
feat(order): add coupon support

- Add Coupon model
- Add coupon validation logic
- Update order total calculation
- Add coupon usage tracking

Closes #123
```

### 5. 错误处理规范

```python
# ✓ 好的错误处理
class OrderNotFoundError(Exception):
    """订单不存在"""
    def __init__(self, order_id: str):
        self.order_id = order_id
        super().__init__(f"Order not found: {order_id}")

def get_order(order_id: str) -> Order:
    try:
        return Order.objects.get(id=order_id)
    except Order.DoesNotExist:
        raise OrderNotFoundError(order_id)

# ❌ 坏的错误处理
def get_order(order_id):
    try:
        return Order.objects.get(id=order_id)
    except:
        return None  # 隐藏错误
```

## 代码规范检查清单

- [ ] 变量命名清晰，有业务含义
- [ ] 函数职责单一，不超过50行
- [ ] 类有清晰的职责和接口
- [ ] 公共API有docstring
- [ ] 错误处理恰当，不捕获通用异常
- [ ] 无硬编码配置
- [ ] Git提交信息规范
- [ ] 代码格式符合团队规范

## 红牌警告

- 提交代码包含TODO且无JIRA链接
- 硬编码密码、密钥、Token
- 删改他人代码未通知
- 提交未测试的代码
- 代码风格与项目规范不一致

## 好/坏对比

**好：**
```python
def calculate_vip_discount(order_amount: Decimal) -> Decimal:
    """计算VIP客户折扣"""
    VIP_DISCOUNT_RATE = Decimal('0.15')
    return order_amount * VIP_DISCOUNT_RATE
```

**坏：**
```python
def calc(x):
    # apply 15% discount for vip
    return x * 0.15
```
