# 零停机部署 (Zero-Downtime Deployment)

## Overview

零停机部署是实现服务不间断部署的技能。包括滚动部署、蓝绿部署、金丝雀发布、回滚策略等。

## 何时使用

- 生产部署
- 版本升级
- 配置变更
- 热更新
- A/B测试

## 流程

1. **部署策略**：选择部署策略
2. **前置检查**：执行部署前检查
3. **流量分割**：分割流量
4. **执行部署**：执行部署
5. **健康检查**：检查服务健康
6. **流量切换**：切换流量
7. **监控验证**：监控验证部署

## 模板

### 零停机部署模板
```python
class ZeroDowntimeDeployment:
    async def rolling_deploy(self, service: Service, new_version: str):
        """滚动部署"""
        # 1. 准备新版本实例
        new_instances = await self.provision(new_version, count=2)

        # 2. 启动健康检查
        for inst in new_instances:
            await self.wait_healthy(inst, timeout=300)

        # 3. 逐步替换
        old_instances = await service.get_instances()
        replace_ratio = 0.25  # 每次替换25%

        for batch in self.batch(old_instances, replace_ratio):
            # 添加新实例
            await service.add_instances(new_instances[:len(batch)])
            # 等待健康
            await asyncio.sleep(30)
            # 移除旧实例
            await service.remove_instances(batch)
            new_instances = new_instances[len(batch):]

        return {"status": "success", "version": new_version}

    async def canary_release(self, service: Service, new_version: str):
        """金丝雀发布"""
        # 1. 部署5%流量
        canary = await self.deploy_canary(service, new_version, 0.05)

        # 2. 监控指标
        metrics = await self.monitor_for(service, canary, duration=600)

        # 3. 分析指标
        if self.is_significant_drift(metrics):
            await self.rollback(canary)
            return {"status": "rollback", "reason": "metrics_drift"}

        # 4. 逐步放大
        for traffic in [0.25, 0.50, 1.0]:
            await service.set_traffic(canary, traffic)
            await asyncio.sleep(300)
            metrics = await self.monitor_for(service, canary, duration=300)

        return {"status": "success", "version": new_version}
```

## 检查清单

- [ ] 策略选择
- [ ] 健康检查
- [ ] 流量控制
- [ ] 监控完善
- [ ] 回滚方案

## 红牌警告

- 部署失败
- 健康检查
- 流量异常
- 回滚失效
