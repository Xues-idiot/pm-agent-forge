# 时间序列分析 (Time Series Analysis)

## Overview

时间序列分析是分析时间相关数据的技能。包括趋势分析、季节性检测、周期分析、预测建模等。

## 何时使用

- 趋势分析
- 销量预测
- 需求预测
- 异常检测
- 季节性分析

## 流程

1. **数据准备**：准备时间序列数据
2. **探索分析**：探索数据特征
3. **趋势分析**：分析趋势
4. **季节性检测**：检测季节性
5. **预测建模**：建立预测模型
6. **异常检测**：检测异常
7. **结果解释**：解释结果

## 模板

### 时间序列分析模板
```python
class TimeSeriesAnalysis:
    async def analyze(self, data: pd.Series):
        """时间序列分析"""
        return {
            "trend": self.decompose_trend(data),
            "seasonality": self.detect_seasonality(data),
            "residual": self.get_residuals(data),
            "stationarity": self.test_stationarity(data)
        }

    async def forecast(self, data: pd.Series, horizon: int):
        """预测"""
        model = await self.fit_model(data, method="prophet")
        forecast = model.predict(horizon)
        return {
            "point_forecast": forecast.values,
            "confidence_interval": forecast.confidence,
            "model": "prophet"
        }

    async def detect_anomalies(self, data: pd.Series):
        """异常检测"""
        from sklearn.ensemble import IsolationForest
        model = IsolationForest(contamination=0.01)
        predictions = model.fit_predict(data.values.reshape(-1, 1))
        return {
            "anomalies": [i for i, p in enumerate(predictions) if p == -1],
            "scores": model.decision_function(data.values.reshape(-1, 1))
        }
```

## 检查清单

- [ ] 数据完整
- [ ] 趋势清晰
- [ ] 季节性准确
- [ ] 预测可靠
- [ ] 异常检测

## 红牌警告

- 数据缺失
- 季节性错误
- 预测偏差
- 异常误报
