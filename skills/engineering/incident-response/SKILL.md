# 故障响应 (Incident Response)

## Overview

故障响应是处理生产环境故障的技能。包括故障检测、应急响应、问题定位、故障恢复、复盘改进等。

## 何时使用

- 生产故障处理
- 应急响应
- 故障复盘
- 预案建设
- SRE实践

## 流程

1. **故障检测**：检测故障发生
2. **应急响应**：启动应急流程
3. **问题定位**：定位故障根因
4. **故障恢复**：执行恢复操作
5. **状态通知**：通知相关方
6. **复盘分析**：复盘故障过程
7. **改进落地**：落实改进措施

## 模板

### 故障响应模板
```python
class IncidentResponse:
    async def handle_incident(self, alert: Alert):
        """处理故障"""
        # 1. 创建故障单
        incident = await self.create_incident(alert)

        # 2. 组建响应团队
        await self.page_oncall(incident)

        # 3. 开始计时
        self.start_timer(incident)

        # 4. 紧急止血
        await self.emergency_fix(incident)

        # 5. 根因分析
        root_cause = await self.analyze_root_cause(incident)

        # 6. 长期修复
        await self.long_term_fix(incident, root_cause)

        # 7. 复盘
        await self.postmortem(incident)

        return incident

    async def emergency_fix(self, incident: Incident):
        """紧急止血"""
        strategies = [
            self.scale_out,      # 扩容
            self.rollback,       # 回滚
            self.circuit_break,  # 熔断
            self.feature_flag    # 特服
        ]
        for strategy in strategies:
            if await strategy.try_execute(incident):
                return True
        return False
```

## 检查清单

- [ ] 检测及时
- [ ] 响应迅速
- [ ] 定位准确
- [ ] 恢复有效
- [ ] 复盘深入

## 红牌警告

- 响应延迟
- 定位错误
- 恢复失败
- 复盘敷衍
