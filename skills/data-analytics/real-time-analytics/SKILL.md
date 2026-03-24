# 实时分析 (Real-time Analytics)

## Overview

实时分析是对数据流进行实时处理的技能。包括流处理、实时计算、实时告警、实时可视化等。

## 何时使用

- 实时监控
- 在线指标
- 实时告警
- 实时推荐
- 实时风控

## 流程

1. **流设计**：设计数据流
2. **处理逻辑**：设计处理逻辑
3. **窗口计算**：设计窗口计算
4. **告警规则**：配置告警规则
5. **实时存储**：配置实时存储
6. **可视化**：设计实时可视化
7. **运维监控**：监控流处理

## 模板

### 实时分析模板
```python
class RealTimeAnalytics:
    def design_stream_processing(self):
        """设计流处理"""
        return {
            "sources": ["kafka", "kinesis", "pulsar"],
            "processing": {
                "engine": "flink",
                " parallelism": 4,
                "checkpoint_interval": "60s"
            },
            "windows": {
                "tumbling": "5min",
                "sliding": "1min/5min",
                "session": "gap:30s"
            },
            "sinks": ["clickhouse", "elasticsearch", "redis"]
        }

    async def calculate_realtime_metrics(self):
        """计算实时指标"""
        return {
            " dau": """
                SELECT COUNT(DISTINCT user_id)
                FROM events
                WHERE window_start >= NOW() - INTERVAL '1' DAY
            """,
            "realtime_revenue": """
                SELECT SUM(amount)
                FROM transactions
                WHERE window_start >= NOW() - INTERVAL '1' HOUR
            """,
            "error_rate": """
                SELECT COUNTIF(status >= 500) * 1.0 / COUNT(*)
                FROM logs
                WHERE window_start >= NOW() - INTERVAL '5' MINUTE
            """
        }

    async def setup_alert(self, metric: str, threshold: float):
        """设置告警"""
        return {
            "metric": metric,
            "condition": f"{metric} > {threshold}",
            "severity": "critical",
            "channels": ["slack", "pagerduty"],
            "cooldown": "5min"
        }
```

## 检查清单

- [ ] 流设计
- [ ] 处理逻辑
- [ ] 窗口计算
- [ ] 告警配置
- [ ] 可视化

## 红牌警告

- 数据延迟
- 处理积压
- 告警误报
- 数据丢失
