---
name: engineering-api-design
description: Use when designing RESTful APIs, GraphQL interfaces, or planning API contracts and versioning strategies.
---

# API Design Skill

设计规范、易用、可扩展的API接口。

## 何时使用

- API接口设计
- 接口规范制定
- API版本管理
- 接口文档编写
- API网关设计

## API设计流程

```
1. 需求分析 → 2. 资源设计 → 3. 接口设计 → 4. 文档输出 → 5. 评审验证
```

### 1. 需求分析

**API设计原则：**

```markdown
## API设计原则

### RESTful原则
| 原则 | 说明 |
|------|------|
| 资源导向 | 用名词不用动词 |
| HTTP方法 | GET/POST/PUT/DELETE |
| 无状态 | 每个请求独立 |
| 标准状态码 | 200/400/404/500等 |

### 设计checklist
- [ ] 接口职责单一
- [ ] 返回结构一致
- [ ] 错误处理规范
- [ ] 版本管理清晰
- [ ] 安全性保障
```

### 2. 资源设计

**资源建模：**

```markdown
## 资源设计

### 资源识别
| 业务实体 | 资源路径 | 说明 |
|---------|---------|------|
| 用户 | /users | 用户资源 |
| 订单 | /orders | 订单资源 |
| 商品 | /products | 商品资源 |

### 资源关系
```
/users/{user_id}/orders    # 用户的所有订单
/products/{product_id}/reviews  # 商品的所有评论
/orders/{order_id}/items      # 订单的所有商品
```

### 资源命名规范
- 使用复数名词：/users 而不是 /user
- 小写+中划线：/user-profiles
- 层级不过深：/orders/123/items 不超过3层
```

### 3. 接口设计

**HTTP方法映射：**

```markdown
## HTTP方法

| 方法 | 用途 | 示例 |
|------|------|------|
| GET | 查询 | GET /users/123 |
| POST | 创建 | POST /users |
| PUT | 全量更新 | PUT /users/123 |
| PATCH | 部分更新 | PATCH /users/123 |
| DELETE | 删除 | DELETE /users/123 |

### 状态码规范
| 状态码 | 含义 | 使用场景 |
|--------|------|---------|
| 200 | 成功 | 正常返回 |
| 201 | 创建成功 | POST创建资源 |
| 204 | 无内容 | DELETE成功 |
| 400 | 参数错误 | 请求参数校验失败 |
| 401 | 未认证 | 缺少token |
| 403 | 无权限 | 权限不足 |
| 404 | 资源不存在 | ID不存在 |
| 500 | 服务器错误 | 系统异常 |
```

**请求/响应设计：**

```markdown
## 请求格式

### Query参数
```
GET /users?status=active&page=1&size=20
```

### Path参数
```
GET /users/{user_id}
```

### 请求体
```json
{
  "username": "string",
  "email": "string",
  "age": "number"
}
```

## 响应格式

### 成功响应
```json
{
  "code": 0,
  "message": "success",
  "data": {
    "id": "123",
    "name": "张三"
  }
}
```

### 分页响应
```json
{
  "code": 0,
  "message": "success",
  "data": {
    "list": [],
    "pagination": {
      "page": 1,
      "size": 20,
      "total": 100,
      "total_pages": 5
    }
  }
}
```

### 错误响应
```json
{
  "code": 40001,
  "message": "参数错误",
  "details": [
    {"field": "email", "message": "邮箱格式不正确"}
  ]
}
```
```

### 4. 文档输出

**OpenAPI规范：**

```markdown
## API文档模板

```yaml
openapi: 3.0.0
info:
  title: 用户服务API
  version: 1.0.0

paths:
  /users:
    get:
      summary: 获取用户列表
      parameters:
        - name: page
          in: query
          schema:
            type: integer
      responses:
        '200':
          description: 成功
```

### 文档内容checklist
- [ ] 接口说明清晰
- [ ] 请求参数完整
- [ ] 响应格式明确
- [ ] 错误码说明
- [ ] 示例完整
```

### 5. 版本管理

**版本策略：**

```markdown
## API版本管理

### 版本路径
```
/api/v1/users
/api/v2/users
```

### 版本策略
| 策略 | 适用场景 | 优缺点 |
|------|---------|--------|
| URL路径 | 主版本 | 清晰但侵入性大 |
| Header | 小版本 | 灵活但不够直观 |
| Query参数 | 简单场景 | 最不推荐 |

### 兼容性
- 添加字段不删除
- 不修改字段类型
- 废弃字段标记
```

## API设计检查清单

- [ ] RESTful规范遵循
- [ ] 命名规范一致
- [ ] 状态码使用正确
- [ ] 错误处理规范
- [ ] 安全性保障
- [ ] 文档完整
- [ ] 版本管理清晰
- [ ] 性能考虑

## 红牌警告

- 接口职责不单一
- 滥用POST做查询
- 错误码混乱
- 安全性漏洞
- 文档过时
- 不兼容变更
- 过度设计
