---
name: engineering-configuration
description: Use when managing configuration systems, feature flags, or environment management. Covers config management, feature toggles, environment promotion, and dynamic configuration.
---

# Configuration Management

配置管理与特性开关。

## 何时使用

- 配置中心设计
- 特性开关管理
- 环境配置管理
- 动态配置
- 配置版本控制

## 配置基础

### 配置类型

```markdown
## 配置类型

### 按用途分类
| 类型 | 说明 | 示例 |
|------|------|------|
| 环境配置 | 不同环境不同 | 数据库/Redis |
| 功能配置 | 功能开关 | 开关特性 |
| 业务配置 | 业务参数 | 阈值/规则 |
| 敏感配置 | 密钥/密码 | API Key |

### 按形式分类
| 类型 | 特点 | 管理 |
|------|------|------|
| 静态配置 | 启动时加载 | 配置文件 |
| 动态配置 | 运行时修改 | 配置中心 |
| 特性开关 | 功能粒度 | Feature Flag |

### 配置原则
```markdown
## 配置原则

### 最佳实践
- 环境隔离：dev/test/prod
- 敏感加密：密码/密钥
- 版本控制：变更可追溯
- 快速生效：无需重启
- 统一管理：集中配置
```
```

## 配置中心

### 架构设计

```markdown
## 配置中心架构

### 核心组件
| 组件 | 职责 | 技术 |
|------|------|------|
| 配置存储 | 持久化配置 | DB/配置库 |
| 配置服务 | 提供配置API | 微服务 |
| 配置推送 | 实时推送 | 长连接 |
| 配置缓存 | 本地缓存 | 本地+远程 |

### 选型对比
| 产品 | 特点 | 适用 |
|------|------|------|
| Apollo | 功能完整 | 大规模 |
| Nacos | 阿里开源 | 微服务 |
| Spring Config | Spring生态 | Spring项目 |
| Consul | Hashicorp | 通用 |
```

### 配置管理

```markdown
## 配置管理

### 配置结构
```json
{
  "application": "order-service",
  "profiles": ["dev", "prod"],
  "namespaces": ["common", "business"]
}
```

### 配置格式
| 格式 | 特点 | 工具 |
|------|------|------|
| Properties | 简单 | Spring |
| YAML | 结构化 | K8s |
| JSON | 复杂结构 | 通用 |
| XML | 层级结构 | 老系统 |
```

## 特性开关

### 开关类型

```markdown
## 特性开关

### 按用途分类
| 类型 | 说明 | 示例 |
|------|------|------|
| 发布开关 | 控制功能发布 | 新功能灰度 |
| 实验开关 | A/B测试 | 开关实验 |
| 运营开关 | 运营配置 | 活动开关 |
| 权限开关 | 权限控制 | VIP功能 |

### 开关粒度
| 粒度 | 说明 | 性能 |
|------|------|------|
| 全局开关 | 所有用户 | 快 |
| 用户群开关 | 特定用户群 | 中 |
| 用户开关 | 单个用户 | 慢 |
```

### 开关实现

```markdown
## 开关实现

### 数据结构
```json
{
  "feature_name": {
    "enabled": true,
    "rules": [
      {
        "type": "percentage",
        "value": 10
      },
      {
        "type": "user_group",
        "value": ["vip", "internal"]
      }
    ]
  }
}
```

### 服务端实现
```java
// 开关判断
if (featureToggle.isEnabled("new_checkout")) {
    // 新逻辑
} else {
    // 老逻辑
}
```
```

### 开关策略

```markdown
## 开关策略

### 灰度策略
| 策略 | 说明 | 风险 |
|------|------|------|
| 百分比灰度 | X%用户 | 逐步放量 |
| 用户群灰度 | 特定用户 | 精准 |
| 地域灰度 | 特定地区 | 本地化 |
| 时间灰度 | 特定时间 | 活动 |

### 降级策略
```markdown
## 降级策略

### 降级场景
- 开关服务不可用
- 开关超时
- 规则计算异常

### 降级方式
- 默认关闭
- 默认打开
- 缓存值
```
```

## 环境管理

### 环境类型

```markdown
## 环境类型

### 标准环境
| 环境 | 用途 | 特点 |
|------|------|------|
| local | 开发 | 本地调试 |
| dev | 开发测试 | 集成测试 |
| test | 测试 | QA验证 |
| staging | 预发布 | 生产验证 |
| prod | 生产 | 正式环境 |

### 环境差异
| 差异 | dev | staging | prod |
|------|-----|---------|------|
| 数据 | Mock | 脱敏 | 真实 |
| 日志 | Debug | Info | Warn |
| 监控 | 简化 | 完整 | 完整 |
| 性能 | 低配 | 中配 | 高配 |
```

### 配置promote

```markdown
## 配置升级

### Promote流程
```markdown
## 环境Promote

dev → test → staging → prod

### 各阶段检查
- dev：功能验证
- test：QA测试
- staging：性能/灰度
- prod：最终验证
```

### 配置差异管理
```json
// application-dev.yml
database.url: localhost:3306

// application-prod.yml
database.url: db.example.com
```
```

## 配置安全

### 敏感配置

```markdown
## 敏感配置

### 敏感内容
| 类型 | 处理方式 |
|------|----------|
| 数据库密码 | 加密存储 |
| API密钥 | 加密存储 |
| 证书密钥 | 加密存储 |
| Token | 加密存储 |

### 安全实践
- 不提交到Git
- 不打印日志
- 加密传输
- 定期轮换
```

### 访问控制

```markdown
## 配置访问控制

### 权限分级
| 角色 | 权限 |
|------|------|
| 开发 | dev环境 |
| 测试 | dev/test |
| 运维 | 全部环境 |
| 管理员 | 全部+审批 |
```

## 检查清单

- [ ] 配置集中管理
- [ ] 特性开关完善
- [ ] 环境隔离清晰
- [ ] 敏感配置加密
- [ ] 变更可追溯
- [ ] 快速生效
- [ ] 容错降级

## 红牌警告

- 配置放代码里
- 密码明文存储
- 无权限控制
- 改配置无记录
- 配置不区分环境
- 配置无容错
- 配置无监控
