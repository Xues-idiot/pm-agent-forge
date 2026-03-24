# 特性开关 (Feature Flag)

## Overview

特性开关是管理功能开关的技能。包括开关设计、灰度发布、A/B测试、动态配置等。

## 何时使用

- 灰度发布
- A/B测试
- 快速回滚
- 动态配置
- 特性控制

## 流程

1. **开关设计**：设计开关结构
2. **实现接入**：接入开关SDK
3. **灰度配置**：配置灰度规则
4. **A/B测试**：配置A/B测试
5. **监控验证**：监控开关效果
6. **持续优化**：优化开关策略
7. **清理下线**：清理废弃开关

## 模板

### 特性开关模板
```python
class FeatureFlag:
    def design_flag_structure(self):
        """设计开关结构"""
        return {
            "flags": {
                "new_checkout_flow": {
                    "description": "新结算流程",
                    "enabled": False,
                    "rules": [
                        {
                            "type": "percentage",
                            "value": 10,
                            "rollout": "2024-01-01"
                        },
                        {
                            "type": "user_segment",
                            "value": "premium_users"
                        }
                    ]
                }
            }
        }

    async def evaluate_flag(self, flag_name: str, context: dict):
        """评估开关"""
        flag = self.get_flag(flag_name)
        user_id = context.get("user_id")
        user_segment = context.get("segment")

        # 检查用户段
        for rule in flag.rules:
            if rule["type"] == "user_segment":
                if user_segment == rule["value"]:
                    return True

        # 检查百分比
        for rule in flag.rules:
            if rule["type"] == "percentage":
                if self.is_in_rollout(user_id, rule["value"]):
                    return True

        return flag.enabled

    async def run_ab_test(self, flag_name: str):
        """运行A/B测试"""
        config = self.get_ab_config(flag_name)
        return {
            "variants": config.variants,
            "distribution": config.distribution,
            "metrics": ["conversion_rate", "revenue", "engagement"],
            "min_sample_size": 1000,
            "duration": "2 weeks"
        }
```

## 检查清单

- [ ] 开关清晰
- [ ] 规则明确
- [ ] 监控完善
- [ ] 回滚方案
- [ ] 清理及时

## 红牌警告

- 开关冲突
- 规则错误
- 监控缺失
- 忘记清理
