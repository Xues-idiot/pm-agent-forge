# 交易通道集成 (Trading Integration)

## Overview

交易通道集成是将下单指令对接实际交易通道的技能。支持模拟交易和实盘交易。

## 何时使用

- 模拟交易测试
- 实盘交易执行
- 交易记录同步
- 账户管理

## 流程

1. **通道选择**：选择交易通道
2. **权限申请**：申请交易权限
3. **接口对接**：对接交易API
4. **订单测试**：测试订单功能
5. **实盘交易**：执行实盘交易
6. **风控检查**：交易前风控
7. **记录同步**：同步交易记录

## 模板

### 交易接口模板
```python
class TradingAPI:
    """统一交易接口"""

    def __init__(self, broker="quant", mode="simulate"):
        self.broker = broker
        self.mode = mode  # simulate/real

    def login(self):
        """登录账户"""
        pass

    def get_account(self):
        """获取账户信息"""
        return {
            "cash": 1000000,  # 可用资金
            "market_value": 500000,  # 市值
            "total": 1500000,  # 总资产
        }

    def get_position(self, stock_code):
        """获取持仓"""
        return {"quantity": 1000, "avg_cost": 10.0}

    def buy(self, stock_code, price, quantity):
        """买入"""
        return {"order_id": "12345", "status": "success"}

    def sell(self, stock_code, price, quantity):
        """卖出"""
        return {"order_id": "12346", "status": "success"}

    def get_orders(self):
        """获取订单"""
        return []

    def get_trades(self):
        """获取成交"""
        return []
```

## 检查清单

- [ ] 通道选择合适
- [ ] 接口稳定
- [ ] 订单正确
- [ ] 风控到位
- [ ] 记录准确
- [ ] 异常处理

## 红牌警告

- 权限申请失败
- 接口不稳定
- 下单错误
- 风控失效
- 记录丢失
- 资金核算错误
