# 天气数据采集 (Weather Data Collection)

## Overview

天气数据采集是从各天气平台采集气象数据的技能。支持历史天气查询、预报数据、极端天气监控等。

## 何时使用

- 气象数据采集
- 极端天气监控
- 历史气候分析
- 农业气象
- 物流调度

## 流程

1. **数据源选择**：选择天气数据源
2. **位置配置**：配置采集位置
3. **实时采集**：采集当前天气
4. **历史查询**：查询历史数据
5. **预报获取**：获取天气预报
6. **极端告警**：监控极端天气
7. **报告生成**：生成分析报告

## 模板

### 天气数据采集模板
```python
class WeatherCollector:
    def __init__(self):
        self.sources = {
            "weatherapi": WeatherAPISpider(),
            "openweathermap": OWMConnector(),
            "cma": ChinaWeatherSpider()
        }

    async def collect_current(self, location: str):
        """采集当前天气"""
        data = {}
        for source_name, source in self.sources.items():
            try:
                data[source_name] = await source.get_current(location)
            except Exception as e:
                data[source_name] = None
        return self.merge_weather_data(data)

    async def get_history(self, location: str, start: date, end: date):
        """获取历史天气"""
        history = []
        current = start
        while current <= end:
            day_data = await self.sources["cma"].get_history(location, current)
            history.append(day_data)
            current += timedelta(days=1)
        return history

    async def monitor_extreme(self, locations: List[str]):
        """监控极端天气"""
        alerts = []
        for location in locations:
            current = await self.collect_current(location)
            if current.is_extreme():
                alerts.append(ExtremeWeatherAlert(
                    location=location,
                    type=current.extreme_type,
                    severity=current.severity,
                    recommendation=current.get_recommendation()
                ))
        return alerts
```

## 检查清单

- [ ] 数据准确
- [ ] 实时更新
- [ ] 覆盖全面
- [ ] 告警及时

## 红牌警告

- 数据错误
- 延迟过高
- 告警遗漏
- 数据缺失
