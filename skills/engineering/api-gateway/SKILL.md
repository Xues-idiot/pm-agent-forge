# API网关设计 (API Gateway Design)

## Overview

API网关设计是设计和管理API网关的技能。包括路由配置、认证授权、限流熔断、协议转换等。

## 何时使用

- 微服务入口
- API统一管理
- 安全防护
- 流量控制
- 协议转换

## 流程

1. **需求分析**：分析API需求
2. **路由设计**：设计路由策略
3. **认证授权**：配置认证授权
4. **限流熔断**：配置限流熔断
5. **监控告警**：配置监控告警
6. **文档生成**：生成API文档
7. **测试验证**：测试验证网关

## 模板

### API网关设计模板
```python
class APIGatewayDesign:
    def design_routing(self, services: List[Service]):
        """设计路由"""
        return {
            "routes": [
                {
                    "path": "/api/users",
                    "service": "user-service",
                    "methods": ["GET", "POST", "PUT", "DELETE"],
                    "timeout": 5000
                },
                {
                    "path": "/api/orders",
                    "service": "order-service",
                    "methods": ["GET", "POST"],
                    "timeout": 10000
                }
            ],
            "middleware": [
                "auth",
                "rate_limit",
                "logging",
                "cors"
            ]
        }

    def design_rate_limit(self):
        """设计限流"""
        return {
            "global": {
                "rate": 10000,
                "burst": 20000
            },
            "per_ip": {
                "rate": 100,
                "burst": 200
            },
            "per_user": {
                "rate": 1000,
                "burst": 2000
            },
            "strategies": ["token_bucket", "leaky_bucket"]
        }

    def design_circuit_breaker(self):
        """设计熔断"""
        return {
            "failure_threshold": 5,
            "success_threshold": 2,
            "timeout": 60,
            "half_open_requests": 3
        }
```

## 检查清单

- [ ] 路由清晰
- [ ] 认证安全
- [ ] 限流合理
- [ ] 熔断有效
- [ ] 监控完善

## 红牌警告

- 路由冲突
- 认证漏洞
- 限流失效
- 熔断误触发
