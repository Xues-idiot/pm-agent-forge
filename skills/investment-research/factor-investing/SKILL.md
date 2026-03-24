# 因子投资分析 (Factor Investing)

## Overview

因子投资分析是识别和利用Alpha因子的技能。通过多因子模型发现超额收益来源。

## 何时使用

- 因子选股
- 因子暴露分析
- 风险归因
- 组合优化

## 流程

1. **因子定义**：定义候选因子
2. **数据准备**：准备因子数据
3. **IC分析**：计算IC/IR
4. **因子有效性**：验证因子有效性
5. **因子合成**：合成复合因子
6. **组合构建**：基于因子构建组合
7. **归因分析**：因子归因分析

## 模板

### 因子分析模板
```python
import pandas as pd
import numpy as np

# 定义因子
FACTORS = {
    'value': ['pe_ratio', 'pb_ratio', 'pcf_ratio'],
    'momentum': ['returns_1m', 'returns_3m', 'returns_6m'],
    'quality': ['roe', 'roa', 'gross_margin'],
    'size': ['market_cap'],
    'volatility': ['volatility_60d', 'beta']
}

def calculate_ic(factor_data: pd.DataFrame, returns: pd.Series) -> pd.DataFrame:
    """计算IC (Information Coefficient)"""
    ic_series = factor_data.corrwith(returns)
    return {
        'ic_mean': ic_series.mean(),
        'ic_std': ic_series.std(),
        'ic_ir': ic_series.mean() / ic_series.std()
    }

def factor_portfolio(factor_data: pd.DataFrame, n_stocks: int = 50):
    """基于因子构建组合"""
    # 因子标准化
    factor_zscore = (factor_data - factor_data.mean()) / factor_data.std()

    # 等权合成
    composite = factor_zscore.mean(axis=1)

    # 选择因子值最高的股票
    selected = composite.nlargest(n_stocks)
    return selected.index.tolist()
```

## 检查清单

- [ ] 因子定义清晰
- [ ] 数据质量可靠
- [ ] IC分析准确
- [ ] 过拟合控制
- [ ] 交易成本考虑
- [ ] 定期再平衡

## 红牌警告

- 因子过拟合
- 数据窥视偏差
- 交易成本忽视
- 容量限制
- 因子失效
