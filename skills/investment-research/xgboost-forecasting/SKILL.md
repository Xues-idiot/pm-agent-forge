# XGBoost价格预测 (XGBoost Price Forecasting)

## Overview

XGBoost价格预测是使用梯度提升树模型预测股价走势的技能。提供量化信号辅助投资决策。

## 何时使用

- 价格趋势预测
- 量化信号生成
- 策略回测验证
- 异常检测预警

## 流程

1. **特征工程**：构建预测特征
2. **标签定义**：定义预测目标
3. **模型训练**：训练XGBoost模型
4. **预测输出**：生成预测结果
5. **信号生成**：生成交易信号
6. **回测验证**：历史回测验证
7. **实盘应用**：应用到实盘

## 模板

### XGBoost预测模板
```python
import xgboost as xgb
import pandas as pd

# 特征工程
FEATURES = [
    # 价格特征
    'returns_5d', 'returns_20d', 'volatility_20d',
    # 技术指标
    'rsi_14', 'macd_signal', 'bb_position',
    # 情绪特征
    'sentiment_score', 'news_count',
    # 宏观特征
    'market_return', 'sector_return'
]

# 模型训练
model = xgb.XGBClassifier(
    n_estimators=100,
    max_depth=6,
    learning_rate=0.1,
    objective='binary:logistic'
)

model.fit(X_train, y_train)

# 预测
predictions = model.predict(X_test)
probabilities = model.predict_proba(X_test)[:, 1]

# 特征重要性
feature_importance = pd.DataFrame({
    'feature': FEATURES,
    'importance': model.feature_importances_
}).sort_values('importance', ascending=False)
```

## 检查清单

- [ ] 特征设计合理
- [ ] 标签定义清晰
- [ ] 模型不过拟合
- [ ] 预测效果验证
- [ ] 回测结果可信
- [ ] 实盘跟踪评估

## 红牌警告

- 过度拟合历史
- 特征泄露
- 忽视流动性
- 交易成本低估
- 过拟合单市场
