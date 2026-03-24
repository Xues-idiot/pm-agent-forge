# 混沌工程 (Chaos Engineering)

## Overview

混沌工程是通过主动注入故障来验证系统韧性的技能。包括故障注入、实验设计、结果分析、改进跟踪等。

## 何时使用

- 系统韧性验证
- 容错能力测试
- 预案验证
- 故障演练
- 韧性建设

## 流程

1. **稳态定义**：定义系统稳态
2. **假设提出**：提出实验假设
3. **实验设计**：设计故障实验
4. **风险评估**：评估实验风险
5. **执行监控**：执行并监控
6. **结果分析**：分析实验结果
7. **改进跟踪**：跟踪改进措施

## 模板

### 混沌工程模板
```python
class ChaosEngineering:
    async def design_experiment(self, service: Service):
        """设计混沌实验"""
        return {
            "steady_state": {
                "metrics": ["latency_p99 < 200ms", "error_rate < 0.1%"],
                "probes": self.setup_probes(service)
            },
            "hypothesis": "如果注入xx故障，系统将yy",
            "experiments": [
                {
                    "name": "kill_instance",
                    "action": "terminate_instance",
                    "target": "random",
                    "rate": 0.1
                },
                {
                    "name": "network_latency",
                    "action": "add_latency",
                    "target": "database",
                    "delay": 500
                }
            ],
            "safety": {
                "max_failure_rate": 0.05,
                "abort_conditions": ["error_rate > 0.5"],
                "rollback": "auto"
            }
        }

    async def run_experiment(self, experiment: Experiment):
        """运行实验"""
        # 前置检查
        await self.preflight_check(experiment)

        # 启动监控
        monitor = await self.start_monitoring(experiment)

        # 执行注入
        await self.inject_fault(experiment)

        # 等待观察
        await asyncio.sleep(experiment.duration)

        # 停止注入
        await self.stop_fault(experiment)

        # 分析结果
        return await self.analyze_results(monitor, experiment)
```

## 检查清单

- [ ] 稳态定义
- [ ] 假设清晰
- [ ] 风险可控
- [ ] 监控完善
- [ ] 改进落实

## 红牌警告

- 风险失控
- 影响生产
- 监控失效
- 改进未落
