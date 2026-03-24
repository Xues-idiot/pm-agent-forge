# A股数据源集成 (A-Share Data Sources)

## Overview

A股数据源集成是将多种数据源（akshare/tushare/东方财富等）整合到投研系统的技能。实现数据的统一采集和管理。

## 何时使用

- 需要获取A股市场数据
- 需要财务、行情、资金流数据
- 需要多数据源交叉验证
- 需要统一的数据接口

## 流程

1. **数据源评估**：评估各数据源优缺点
2. **接口设计**：设计统一数据接口
3. **采集实现**：实现各数据源采集
4. **数据清洗**：标准化数据格式
5. **质量校验**：校验数据准确性
6. **缓存管理**：设计缓存策略
7. **监控告警**：监控采集状态

## 模板

### 数据源配置模板
```python
# 数据源配置
DATA_SOURCES = {
    "akshare": {
        "strengths": ["行情数据全", "免费", "接口稳定"],
        "weaknesses": ["财务数据少", "需要本地缓存"],
        "rate_limit": "10次/秒",
        "use_cases": ["实时行情", "基金数据", "宏观数据"]
    },
    "tushare": {
        "strengths": ["财务数据全", "公告数据", "资金流"],
        "weaknesses": ["需要token", "有积分限制"],
        "rate_limit": "根据积分"],
        "use_cases": ["财务报表", "公告", "融资融券"]
    },
    "eastmoney": {
        "strengths": ["资金流数据", "实时性强"],
        "weaknesses": ["格式复杂"],
        "use_cases": ["北向资金", "主力资金"]
    }
}

# 统一数据接口
class StockDataAPI:
    def __init__(self):
        self.akshare = AkshareAdapter()
        self.tushare = TushareAdapter()

    def get_price(self, stock_code: str, period: str = "daily"):
        """获取价格数据"""
        return self.akshare.get_price(stock_code, period)

    def get_financial(self, stock_code: str, years: list):
        """获取财务数据"""
        return self.tushare.get_financial(stock_code, years)

    def get_cashflow(self, stock_code: str):
        """获取资金流数据"""
        return self.eastmoney.get_cashflow(stock_code)
```

## 检查清单

- [ ] 数据源选择合理
- [ ] 接口设计统一
- [ ] 错误处理完善
- [ ] 缓存策略有效
- [ ] 监控到位
- [ ] 文档清晰

## 红牌警告

- 单一数据源依赖
- 缺乏数据校验
- API调用超限
- 数据格式不统一
- 缓存过期未处理
