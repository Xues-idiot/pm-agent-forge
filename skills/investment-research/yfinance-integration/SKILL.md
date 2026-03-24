# Yahoo Finance数据集成 (Yahoo Finance Integration)

## Overview

Yahoo Finance数据集成是通过yfinance库获取全球市场数据的技能。支持港股、美股、期货、加密货币等。

## 何时使用

- 获取美股实时数据
- 获取港股数据
- 获取期货数据
- 获取加密货币数据

## 流程

1. **库安装**：安装yfinance
2. **数据获取**：获取各类数据
3. **数据清洗**：清洗数据
4. **本地存储**：存储到本地
5. **增量更新**：增量更新
6. **质量校验**：校验数据
7. **API封装**：封装接口

## 模板

### yfinance模板
```python
import yfinance as yf

def get_us_stock_data(ticker: str, period: str = "1y"):
    """获取美股数据"""
    stock = yf.Ticker(ticker)
    data = stock.history(period=period)
    return data

def get_financials(ticker: str):
    """获取财务报表"""
    stock = yf.Ticker(ticker)
    financials = {
        'income_stmt': stock.income_stmt,
        'balance_sheet': stock.balance_sheet,
        'cashflow': stock.cashflow,
    }
    return financials

def get_analyst_info(ticker: str):
    """获取分析师信息"""
    stock = yf.Ticker(ticker)
    recommendations = stock.recommendations
    target_price = stock.target_mean_value
    return {'recommendations': recommendations, 'target_price': target_price}

# 示例
msft = yf.Ticker("MSFT")
print(msft.info)  # 基本信息
print(msft.history(period="1mo"))  # 月线数据
```

## 检查清单

- [ ] 数据获取稳定
- [ ] 数据格式正确
- [ ] 错误处理完善
- [ ] 缓存策略有效
- [ ] 增量更新正确
- [ ] 配额限制处理

## 红牌警告

- API限制
- 数据延迟
- 格式变化
- 网络问题
- 配额超限
