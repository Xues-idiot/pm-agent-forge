---
name: engineering-devops
description: Use when managing DevOps practices, CI/CD pipelines, or infrastructure automation. Covers CI/CD design, container orchestration, infrastructure as code, and monitoring.
---

# DevOps Practices

DevOps实践与自动化。

## 何时使用

- CI/CD流水线设计
- 容器编排
- 基础设施即代码
- 自动化运维
- 发布策略

## CI/CD设计

### 流水线

```markdown
## CI/CD流水线

### 阶段设计
| 阶段 | 内容 | 工具 |
|------|------|------|
| Build | 编译打包 | Maven/Gradle |
| Test | 单元测试 | JUnit/Pytest |
| Scan | 代码扫描 | SonarQube |
| Security | 安全扫描 | Trivy |
| Deploy | 部署 | Ansible/K8s |
| Verify | 验证 | 自动测试 |

### 流水线类型
| 类型 | 特点 | 适用 |
|------|------|------|
| 串行 | 顺序执行 | 简单项目 |
| 并行 | 多任务并行 | 复杂项目 |
| 矩阵 | 参数组合 | 多环境 |

### 触发方式
| 触发 | 说明 | 配置 |
|------|------|------|
| Push | 代码提交 | 分支规则 |
| PR | Merge请求 | 合并检查 |
| Tag | 版本发布 | 发布流程 |
| Schedule | 定时执行 | Cron |
| Manual | 手动触发 | 审批流程 |
```

### GitFlow分支策略

```markdown
## 分支策略

### 分支模型
| 分支 | 用途 | 命名 |
|------|------|------|
| main | 主分支 | main/master |
| release | 发布分支 | release/* |
| develop | 开发分支 | develop |
| feature | 功能分支 | feature/* |
| hotfix | 热修复 | hotfix/* |

### 流程
```markdown
## 开发流程

1. 从develop创建feature分支
2. feature开发并测试
3. 合并回develop
4. 从develop创建release分支
5. release测试和修复
6. 合并到main和develop
7. 打tag发布
```
```

## 容器编排

### Docker最佳实践

```markdown
## Docker实践

### Dockerfile优化
| 优化项 | 方法 | 效果 |
|--------|------|------|
| 多阶段构建 | 分离构建 | 减小镜像 |
| 减少层 | 合并指令 | 减小体积 |
| 基础镜像 |  alpine | 减小体积 |
| .dockerignore | 排除文件 | 减小体积 |
| 顺序执行 | 缓存优化 | 构建加速 |

### 镜像大小控制
```dockerfile
## 优化示例

# 使用多阶段构建
FROM golang:1.21 AS builder
WORKDIR /app
COPY . .
RUN go build -o service

# 最终镜像
FROM alpine:3.19
COPY --from=builder /app/service /usr/local/bin/
CMD ["service"]
```

### 健康检查
```dockerfile
## 健康检查
HEALTHCHECK --interval=30s --timeout=3s \
  --start-period=5s --retries=3 \
  CMD curl -f http://localhost:8080/health || exit 1
```
```

### Kubernetes

```markdown
## K8s实践

### 资源管理
| 资源 | 说明 | 设置 |
|------|------|------|
| Pod | 最小调度单位 | 副本数 |
| Deployment | 无状态部署 | replicas |
| StatefulSet | 有状态部署 | 持久存储 |
| DaemonSet | 节点守护 | 日志/监控 |

### 资源限制
| 限制 | 说明 | 设置原则 |
|------|------|----------|
| requests | 最低需求 | 正常使用 |
| limits | 最大限制 | 防止异常 |
| Liveness | 存活探针 | 自动重启 |
| Readiness | 就绪探针 | 流量调度 |

### 滚动更新
```yaml
## 滚动更新策略
spec:
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
```
```

## 基础设施即代码

### IaC工具

```markdown
## IaC工具

### 工具对比
| 工具 | 特点 | 适用 |
|------|------|------|
| Terraform | 云无关 | 多云 |
| Pulumi | 代码化 | 开发者友好 |
| Ansible | 幂等 | 配置管理 |
| Helm | K8s包管理 | 应用部署 |

### Terraform实践
```terraform
## 模块化设计

# 模块调用
module "ecs" {
  source = "./modules/ecs"
  cluster = var.cluster
  desired_count = var.instance_count
  environment = var.environment
}

# 状态管理
terraform {
  backend "s3" {
    bucket = "tf-state"
    key = "prod/ecs.tfstate"
  }
}
```
```

## 发布策略

### 部署方式

```markdown
## 部署策略

### 蓝绿部署
| 步骤 | 操作 | 优点 |
|------|------|------|
| 1 | 部署绿色环境 | 无停机 |
| 2 | 流量切换 | 快速回滚 |
| 3 | 观察验证 | 零风险 |
| 4 | 下线蓝色 | 资源释放 |

### 金丝雀发布
| 阶段 | 流量 | 目的 |
|------|------|------|
| 1% | 1%流量 | 小范围验证 |
| 10% | 10%流量 | 扩大验证 |
| 50% | 50%流量 | 主要验证 |
| 100% | 全量 | 完全切换 |

### 滚动发布
| 策略 | 说明 | 适用 |
|------|------|------|
| 滚动更新 | 逐步替换 | K8s默认 |
| 不可中断 | 需全部就绪 | 严格要求 |
```

## 监控告警

### 监控体系

```markdown
## 监控体系

### 四大指标（USE）
| 类型 | 说明 | 指标 |
|------|------|------|
| Utilization | 利用率 | CPU/内存 |
| Saturation | 饱和度 | 队列长度 |
| Errors | 错误率 | 5xx/异常 |

### RED方法
| 指标 | 说明 | 监控 |
|------|------|------|
| Rate | 请求率 | QPS |
| Errors | 错误率 | 5xx |
| Duration | 响应时间 | P99 |

### 监控工具
| 工具 | 用途 | 特点 |
|------|------|------|
| Prometheus | 指标采集 | 云原生 |
| Grafana | 可视化 | 丰富图表 |
| Loki | 日志收集 | 成本低 |
| Jaeger | 链路追踪 | 分布式 |

### 告警策略
| 策略 | 说明 | 配置 |
|------|------|------|
| 静态阈值 | 固定值 | 简单 |
| 动态阈值 | 趋势判断 | 复杂 |
| 同比环比 | 历史对比 | 业务 |
| 多条件 | 组合判断 | 精确 |
```

## 检查清单

- [ ] CI/CD流水线完善
- [ ] 分支策略清晰
- [ ] Docker镜像优化
- [ ] K8s配置规范
- [ ] IaC实践到位
- [ ] 发布策略安全
- [ ] 监控告警健全

## 红牌警告

- 无CI/CD流水线
- 手动部署
- 镜像无版本管理
- 无回滚方案
- 监控缺失
- 无告警机制
- secrets明文存储
