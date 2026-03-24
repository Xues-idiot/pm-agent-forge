# 订阅监控 (Subscription Monitoring)

## Overview

订阅监控是追踪和管理播客订阅更新的技能。

## 何时使用

- 追踪新内容
- 更新提醒
- 定时下载
- 批量管理

## 流程

1. **订阅管理**：管理订阅列表
2. **更新检测**：检测播客更新
3. **新Episode发现**：发现新Episode
4. **告警通知**：发送通知
5. **自动下载**：自动下载
6. **历史记录**：记录历史
7. **统计分析**：统计分析

## 模板

### 订阅监控配置
```python
MONITORING_CONFIG = {
    "check_interval": 3600,  # 每小时检查
    "auto_download": True,
    "download_quality": "high",
    "notify_on_new": True,
    "batch_size": 3  # 每次最多下载3个
}

async def monitor_subscriptions():
    """监控订阅"""
    subscriptions = await get_all_subscriptions()

    for sub in subscriptions:
        # 检查更新
        latest = await check_for_updates(sub.rss_url)

        if latest and latest > sub.last_checked:
            # 发现新Episode
            await notify_new_episode(sub, latest)

            if MONITORING_CONFIG["auto_download"]:
                await download_episode(latest, limit=3)

            # 更新记录
            await update_subscription(sub.id, latest)
```

## 检查清单

- [ ] 检查及时
- [ ] 更新发现
- [ ] 通知准确
- [ ] 下载稳定
- [ ] 记录完整
- [ ] 统计准确

## 红牌警告

- 检查延迟
- 更新遗漏
- 通知失败
- 下载失败
- 记录丢失
- 频率过高
