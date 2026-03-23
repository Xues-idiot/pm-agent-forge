---
name: engineering-backend-patterns
description: Use when designing backend systems, choosing architecture patterns, or implementing server-side solutions. Covers REST APIs, microservices, databases, and common patterns.
---

# Backend Patterns

后端设计模式，设计和实现服务端架构。

## 何时使用

- 后端架构设计
- API设计
- 数据库设计
- 服务架构选择
- 微服务设计

## API设计

### RESTful原则

```markdown
## RESTful API

### 资源命名
| 实践 | 示例 |
|------|------|
| 用名词 | /users |
| 复数形式 | /users |
| 嵌套资源 | /users/123/orders |
| 用横线 | /user-profiles |

### HTTP方法
| 方法 | 用途 | 示例 |
|------|------|------|
| GET | 查询 | GET /users |
| POST | 创建 | POST /users |
| PUT | 全量更新 | PUT /users/123 |
| PATCH | 部分更新 | PATCH /users/123 |
| DELETE | 删除 | DELETE /users/123 |

### 状态码
| 状态码 | 含义 |
|--------|------|
| 200 | 成功 |
| 201 | 创建成功 |
| 400 | 请求错误 |
| 401 | 未认证 |
| 403 | 无权限 |
| 404 | 资源不存在 |
| 500 | 服务器错误 |
```

### API版本管理

```markdown
## API版本

### 版本策略
| 策略 | 示例 | 适用 |
|------|------|------|
| URL路径 | /api/v1/users | 通用 |
| Query参数 | /api/users?version=1 | 简单场景 |
| Header | Accept: v1 | RESTful |

### 版本迁移
1. 维护多版本并存
2. 旧版本标记废弃
3. 提供迁移指南
4. 设置淘汰时间
```

## 数据库设计

### 设计原则

```markdown
## 数据库设计

### 范式
| 范式 | 要求 | 适用 |
|------|------|------|
| 1NF | 原子性 | 必达 |
| 2NF | 无部分依赖 | 必达 |
| 3NF | 无传递依赖 | 推荐 |

### 命名规范
```markdown
## 命名规范

### 表名
- 小写下划线
- 复数名词
- 模块前缀

### 字段
- id: 主键
- created_at: 创建时间
- updated_at: 更新时间
- deleted_at: 软删除

### 示例
users, user_profiles, orders, order_items
```
```

### 索引设计

```markdown
## 索引设计

### 索引类型
| 类型 | 适用 |
|------|------|
| 主键索引 | 唯一 |
| 唯一索引 | 唯一约束 |
| 普通索引 | 查询加速 |
| 组合索引 | 多字段查询 |

### 设计原则
- 查询条件字段加索引
- 区分度高的字段
- 不要过度索引
- 定期维护索引
```

## 架构模式

### 单体架构

```markdown
## 单体架构

### 特点
- 单一部署单元
- 共享数据库
- 开发简单
- 适合小型项目

### 适用场景
- 小型项目
- 团队小
- 快速迭代
```

### 微服务架构

```markdown
## 微服务架构

### 特点
- 服务独立部署
- 独立数据库
- 按业务划分
- 服务间通信

### 适用场景
- 大型项目
- 团队大
- 高并发
- 需要弹性

### 设计原则
```markdown
## 微服务设计原则

### 划分原则
- 单一职责
- 高内聚低耦合
- 边界清晰

### 通信方式
- 同步：HTTP/gRPC
- 异步：消息队列

### 数据管理
- 每个服务独立数据库
- 通过API通信
- 避免分布式事务
```
```

### 事件驱动架构

```markdown
## 事件驱动

### 组件
| 组件 | 作用 |
|------|------|
| 事件发布者 | 产生事件 |
| 事件总线 | 路由事件 |
| 事件订阅者 | 处理事件 |

### 适用场景
- 异步处理
- 解耦服务
- 数据同步
```

## 设计模式

### 常见模式

```markdown
## 常用模式

### 工厂模式
```python
class UserFactory:
    @staticmethod
    def create(type):
        if type == "admin":
            return Admin()
        return NormalUser()
```

### 单例模式
```python
class Config:
    _instance = None

    @classmethod
    def get_instance(cls):
        if cls._instance is None:
            cls._instance = cls()
        return cls._instance
```

### 仓储模式
```python
class UserRepository:
    def __init__(self, db):
        self.db = db

    def get(self, id):
        return self.db.query("SELECT * FROM users WHERE id = ?", id)
```
```

### 策略模式

```markdown
## 策略模式

### 场景
不同支付方式、不同算法可以切换

```python
class PaymentStrategy:
    def pay(self, amount):
        raise NotImplementedError

class Alipay(PaymentStrategy):
    def pay(self, amount):
        # 支付宝支付
        pass

class WechatPay(PaymentStrategy):
    def pay(self, amount):
        # 微信支付
        pass

class Order:
    def set_payment(self, strategy):
        self.strategy = strategy

    def pay(self, amount):
        self.strategy.pay(amount)
```
```

## 安全设计

### 认证授权

```markdown
## 安全设计

### 认证方式
| 方式 | 适用 |
|------|------|
| JWT | API认证 |
| Session | Web应用 |
| OAuth | 第三方登录 |
| API Key | 服务间调用 |

### 授权模型
```markdown
## RBAC模型

### 表结构
- users: 用户
- roles: 角色
- permissions: 权限
- user_roles: 用户角色关系
- role_permissions: 角色权限关系
```
```

### 数据安全

```markdown
## 数据安全

### 敏感数据
- 密码加密存储
- 敏感信息脱敏
- 日志脱敏
- 传输加密(HTTPS)

### SQL注入防护
- 参数化查询
- ORM使用
- 输入验证
```

## 性能优化

### 缓存策略

```markdown
## 缓存设计

### 缓存层级
| 层级 | 介质 | 适用 |
|------|------|------|
| 本地缓存 | 内存 | 热点数据 |
| 分布式缓存 | Redis | 共享数据 |
| CDN | 边缘节点 | 静态资源 |

### 缓存策略
```markdown
## 缓存策略

### Cache-Aside
1. 读：缓存命中返回，否则查库并写入缓存
2. 写：更新数据库，删除缓存

### Write-Behind
1. 写：写入缓存
2. 异步写数据库
```
```

### 数据库优化

```markdown
## 数据库优化

### 常用手段
- 索引优化
- 查询优化
- 分库分表
-读写分离

### 慢查询分析
1. 开启慢查询日志
2. 分析执行计划
3. 优化索引
4. 优化SQL
```

## 检查清单

- [ ] API设计RESTful
- [ ] 数据库设计规范
- [ ] 错误处理完善
- [ ] 安全措施到位
- [ ] 缓存策略合理
- [ ] 日志记录完整

## 红牌警告

- SQL注入漏洞
- 敏感数据明文
- 错误信息泄露
- 无限流保护
- 无日志记录
- 接口无版本控制