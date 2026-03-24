# 期权分析 (Options Analysis)

## Overview

期权分析是分析期权定价和希腊字母的技能。为投资决策提供风险管理和收益增强视角。

## 何时使用

- 风险对冲分析
- 收益增强策略
- 波动率交易
- 结构化产品设计

## 流程

1. **期权链获取**：获取期权链数据
2. **定价分析**：分析期权价格
3. **希腊字母**：计算Greeks
4. **波动率分析**：分析隐含波动率
5. **策略设计**：设计交易策略
6. **风险评估**：评估风险
7. **执行监控**：执行和监控

## 模板

### 期权分析模板
```python
from scipy.stats import norm
import numpy as np

def black_scholes(S, K, T, r, sigma, option_type='call'):
    """Black-Scholes期权定价"""
    d1 = (np.log(S/K) + (r + sigma**2/2)*T) / (sigma*np.sqrt(T))
    d2 = d1 - sigma*np.sqrt(T)

    if option_type == 'call':
        price = S*norm.cdf(d1) - K*np.exp(-r*T)*norm.cdf(d2)
    else:
        price = K*np.exp(-r*T)*norm.cdf(-d2) - S*norm.cdf(-d1)

    return price

def calculate_greeks(S, K, T, r, sigma):
    """计算希腊字母"""
    d1 = (np.log(S/K) + (r + sigma**2/2)*T) / (sigma*np.sqrt(T))
    d2 = d1 - sigma*np.sqrt(T)

    delta = norm.cdf(d1)
    gamma = norm.pdf(d1) / (S * sigma * np.sqrt(T))
    theta = -(S * norm.pdf(d1) * sigma) / (2*np.sqrt(T)) - r*K*np.exp(-r*T)*norm.cdf(d2)
    vega = S * np.sqrt(T) * norm.pdf(d1)

    return {'delta': delta, 'gamma': gamma, 'theta': theta, 'vega': vega}
```

## 检查清单

- [ ] 定价模型正确
- [ ] Greeks计算准确
- [ ] 波动率分析合理
- [ ] 策略设计合适
- [ ] 风险评估到位
- [ ] 监控及时

## 红牌警告

- 模型假设不成立
- 波动率估计错误
- 流动性风险
- 保证金风险
- 操作风险
