---
name: engineering-security-design
description: Use when designing security architecture, implementing authentication/authorization, or planning security controls.
---

# Security Design Skill

设计安全可靠的软件系统。

## 何时使用

- 安全架构设计
- 认证授权实现
- 数据安全规划
- 安全漏洞修复
- 合规要求设计

## 安全设计流程

```
1. 威胁建模 → 2. 安全设计 → 3. 防护实现 → 4. 安全测试 → 5. 监控运维
```

### 1. 威胁建模

**STRIDE模型：**

```markdown
## STRIDE威胁分类

| 威胁类型 | 描述 | 对应防护 |
|---------|------|---------|
| Spoofing | 伪装身份 | 认证 |
| Tampering | 篡改数据 | 完整性校验 |
| Repudiation | 否认行为 | 数字签名/审计日志 |
| Information Disclosure | 信息泄露 | 加密 |
| Denial of Service | 服务拒绝 | 限流/高可用 |
| Elevation of Privilege | 权限提升 | 最小权限原则 |

### 常见威胁
```markdown
## 威胁建模步骤

1. 识别资产
   - 用户数据
   - 交易数据
   - 敏感配置

2. 识别入口点
   - API接口
   - Web界面
   - 消息队列

3. 识别信任边界
   - 外部网络 ↔ 内部网络
   - 用户层 ↔ 数据层

4. 识别威胁
   - SQL注入
   - XSS攻击
   - CSRF攻击
```
```

### 2. 安全设计

**认证设计：**

```markdown
## 认证设计

### 密码存储
```python
# 正确方式：使用bcrypt
import bcrypt

def hash_password(password: str) -> str:
    salt = bcrypt.gensalt()
    return bcrypt.hashpw(password.encode(), salt).decode()

def verify_password(password: str, hashed: str) -> bool:
    return bcrypt.checkpw(password.encode(), hashed.encode())

# 错误方式：不要使用MD5/SHA1做密码哈希
# 也不要只做简单加盐
```

### JWT Token
```python
import jwt
from datetime import datetime, timedelta

SECRET_KEY = "your-secret-key"  # 环境变量存储

def create_token(user_id: int) -> str:
    payload = {
        "user_id": user_id,
        "exp": datetime.utcnow() + timedelta(hours=24),
        "iat": datetime.utcnow()
    }
    return jwt.encode(payload, SECRET_KEY, algorithm="HS256")

def verify_token(token: str) -> dict:
    try:
        return jwt.decode(token, SECRET_KEY, algorithms=["HS256"])
    except jwt.ExpiredSignatureError:
        raise TokenExpiredError()
    except jwt.InvalidTokenError:
        raise InvalidTokenError()
```

### OAuth 2.0流程
```markdown
## OAuth 2.0授权码流程

1. 用户点击"使用Google登录"
2. 跳转到Google授权页面
3. 用户授权
4. 返回授权码到回调URL
5. 后端用授权码换取Access Token
6. 用Access Token获取用户信息
7. 创建/关联本地用户
```
```

**授权设计：**

```markdown
## 授权设计

### RBAC模型
```python
# 角色定义
class Role:
    ADMIN = "admin"
    USER = "user"
    GUEST = "guest"

# 权限定义
PERMISSIONS = {
    "user:read": [Role.ADMIN, Role.USER],
    "user:write": [Role.ADMIN],
    "user:delete": [Role.ADMIN],
    "order:read": [Role.ADMIN, Role.USER, Role.GUEST],
    "order:write": [Role.ADMIN, Role.USER],
}

# 权限检查
def require_permission(permission: str):
    def decorator(func):
        @wraps(func)
        def wrapper(user, *args, **kwargs):
            if user.role not in PERMISSIONS.get(permission, []):
                raise PermissionDeniedError()
            return func(user, *args, **kwargs)
        return wrapper
    return decorator

@require_permission("user:write")
def update_user(user_id: int, data: dict):
    pass
```

### 最小权限原则
```markdown
## 最小权限实践

1. 默认拒绝
2. 粒度化权限
3. 临时权限
4. 定期审查
5. 权限分离
```
```

### 3. 防护实现

**输入验证：**

```python
## 输入验证

from pydantic import BaseModel, validator

class UserInput(BaseModel):
    email: str
    password: str
    age: int

    @validator('email')
    def validate_email(cls, v):
        if '@' not in v:
            raise ValueError('Invalid email')
        return v.lower()

    @validator('password')
    def validate_password(cls, v):
        if len(v) < 8:
            raise ValueError('Password too short')
        if not any(c.isupper() for c in v):
            raise ValueError('Need uppercase')
        return v

    @validator('age')
    def validate_age(cls, v):
        if v < 0 or v > 150:
            raise ValueError('Invalid age')
        return v
```

**SQL注入防护：**

```python
# 使用参数化查询
def get_user_by_email(email: str):
    # 正确：参数化查询
    query = "SELECT * FROM users WHERE email = %s"
    cursor.execute(query, (email,))

    # 错误：字符串拼接
    # query = f"SELECT * FROM users WHERE email = '{email}'"
```

**XSS防护：**

```python
# HTML转义
import html

def escape_html(text: str) -> str:
    return html.escape(text)

# 在模板中
# {{ user_input | escape }}  (Jinja2)
# {userInput}  (React会自动转义)
```

**CSRF防护：**

```python
# CSRF Token
from flask_wtf import CSRFProtect

app = Flask(__name__)
CSRFProtect(app)

# 表单中
# <input type="hidden" name="csrf_token" value="{{ csrf_token() }}"/>
```

### 4. 安全测试

**安全测试清单：**

```markdown
## 安全测试checklist

### 认证测试
- [ ] 暴力破解防护
- [ ] 密码强度验证
- [ ] Token过期处理
- [ ] 会话管理安全

### 授权测试
- [ ] 水平越权检查
- [ ] 垂直越权检查
- [ ] 权限继承验证

### 输入测试
- [ ] SQL注入测试
- [ ] XSS测试
- [ ] 命令注入测试
- [ ] 文件上传安全

### 数据安全
- [ ] 敏感数据加密
- [ ] 日志脱敏
- [ ] 备份安全
```

### 5. 监控运维

**安全监控：**

```markdown
## 安全监控指标

| 指标 | 告警阈值 |
|------|---------|
| 失败登录次数 | >10次/分钟 |
| 异常IP访问 | 新IP突然大量请求 |
| 权限滥用 | 普通用户访问管理接口 |
| 数据异常导出 | 大批量数据导出 |
```

## 安全设计检查清单

- [ ] 威胁建模完成
- [ ] 认证机制安全
- [ ] 授权粒度合理
- [ ] 输入验证完善
- [ ] 敏感数据加密
- [ ] 日志审计完整
- [ ] 安全更新机制
- [ ] 应急响应预案

## 红牌警告

- 密码明文存储
- SQL拼接用户输入
- 权限检查缺失
- 敏感数据日志
- 密钥硬编码
- 第三方依赖漏洞
- 安全配置不当
- 无入侵检测
