# 监控告警 (Monitoring & Alerting)

## Overview

监控告警是设置系统监控和价格告警的技能。及时发现投资机会和风险。

## 何时使用

- 设置价格监控
- 设置异动告警
- 持仓跟踪
- 市场监控

## 流程

1. **监控需求**：确定监控目标
2. **阈值设置**：设置告警阈值
3. **监控配置**：配置监控规则
4. **告警通道**：配置告警通知
5. **测试验证**：测试告警
6. **优化调整**：优化阈值
7. **持续运行**：7x24运行

## 模板

### 监控配置模板
```python
# 监控配置
MONITORING_CONFIG = {
    # 价格告警
    "price_alerts": [
        {"stock": "600519", "above": 2000, "below": 1800},
        {"stock": "000858", "above": 300, "below": 250},
    ],

    # 涨跌幅告警
    "change_alerts": [
        {"stock": "600519", "change_pct": 5},  # 日涨幅超5%
    ],

    # 成交量告警
    "volume_alerts": [
        {"stock": "600519", "volume_ratio": 3},  # 量比超3
    ],

    # 新闻舆情告警
    "news_alerts": [
        {"keywords": ["贵州茅台", "业绩"], "sentiment": "negative"},
    ],

    # 财务数据告警
    "financial_alerts": [
        {"stock": "600519", "indicator": "revenue_yoy", "threshold": 10},
    ]
}

# 告警通知配置
ALERT_CHANNELS = {
    "email": {"enabled": True, "recipients": ["user@example.com"]},
    "wechat": {"enabled": True, "webhook": "https://..."},
    "sms": {"enabled": False}
}
```

## 检查清单

- [ ] 阈值设置合理
- [ ] 告警及时
- [ ] 通知到位
- [ ] 无误报
- [ ] 无漏报
- [ ] 记录完整

## 红牌警告

- 阈值过窄告警过多
- 阈值过宽漏报
- 告警通知失败
- 监控遗漏重要标的
- 历史记录缺失
