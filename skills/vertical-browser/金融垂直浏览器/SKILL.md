# 金融垂直浏览器 (Financial Browser)

## Overview

金融垂直浏览器是专门用于金融数据采集和分析的技能。支持东方财富、同花顺、雪球等平台。

## 何时使用

- 股票行情监控
- 财报数据采集
- 基金数据跟踪
- 债券市场分析
- 期货数据监控

## 流程

1. **平台选择**：选择金融数据平台
2. **数据定位**：定位目标数据
3. **数据采集**：采集金融数据
4. **数据校验**：校验数据准确性
5. **数据分析**：分析数据趋势
6. **监控告警**：设置价格告警
7. **报告生成**：生成分析报告

## 模板

### 金融数据采集模板
```python
class FinancialBrowser:
    def __init__(self):
        self.platforms = {
            "eastmoney": EastMoneySpider(),
            "ths": THSSpider(),
            "xueqiu": XueqiuSpider()
        }

    async def get_stock_data(self, symbol: str, period: str):
        """获取股票数据"""
        stock_data = await self.platforms["eastmoney"].get_kline(symbol, period)
        return self.normalize_stock_data(stock_data)

    async def get_financial_report(self, symbol: str, year: int):
        """获取财务报表"""
        report = await self.platforms["eastmoney"].get_report(symbol, year)
        return self.parse_financial_statement(report)

    async def monitor_stock_price(self, symbols: List[str], threshold: float):
        """监控股票价格"""
        alerts = []
        for symbol in symbols:
            current = await self.get_realtime_price(symbol)
            original = self.get_baseline_price(symbol)
            if abs(current - original) / original > threshold:
                alerts.append(PriceAlert(symbol, current, original))
        return alerts
```

## 检查清单

- [ ] 数据准确
- [ ] 实时性
- [ ] 覆盖全面
- [ ] 分析深入
- [ ] 告警及时
- [ ] 报告专业

## 红牌警告

- 数据延迟
- 数据错误
- 封号风险
- 分析偏差
- 告警失效
