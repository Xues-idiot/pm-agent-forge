# 密钥管理 (Secret Management)

## Overview

密钥管理是管理密钥和敏感配置的技能。包括密钥轮换、加密存储、访问控制、审计日志等。

## 何时使用

- 密钥管理
- 凭证轮换
- 安全审计
- 合规检查
- 密钥泄露处理

## 流程

1. **密钥分类**：分类密钥类型
2. **存储设计**：设计存储方案
3. **访问控制**：设置访问策略
4. **轮换策略**：制定轮换策略
5. **审计日志**：配置审计日志
6. **泄露处理**：制定泄露处理
7. **合规检查**：检查合规性

## 模板

### 密钥管理模板
```python
class SecretManagement:
    def design_secret_rotation(self):
        """设计密钥轮换"""
        return {
            "api_keys": {
                "rotation_period": "90d",
                "grace_period": "7d",
                "notification": "3d"
            },
            "db_passwords": {
                "rotation_period": "30d",
                "grace_period": "1d",
                "notification": "1d"
            },
            "certificates": {
                "rotation_period": "365d",
                "grace_period": "30d",
                "notification": "7d"
            }
        }

    async def rotate_secret(self, secret_name: str):
        """轮换密钥"""
        # 生成新密钥
        new_secret = await self.generate_secret(secret_name)

        # 更新配置中心
        await self.config_center.update(secret_name, new_secret)

        # 通知相关服务
        await self.notify_services(secret_name)

        # 等待确认
        await self.wait_for_ack(timeout=300)

        # 验证
        if await self.verify_rotation(secret_name):
            await self.deprecate_old_secret(secret_name)
        else:
            await self.rollback_rotation(secret_name)

    async def handle_leak(self, secret_name: str):
        """处理密钥泄露"""
        # 立即轮换
        await self.rotate_secret(secret_name)

        # 检查使用记录
        usage = await self.get_usage_logs(secret_name)

        # 评估泄露风险
        risk = self.assess_leak_risk(usage)

        # 如果高风险，重置所有相关密钥
        if risk == "high":
            await self.reset_all_related(secret_name)
```

## 检查清单

- [ ] 分类清晰
- [ ] 存储安全
- [ ] 轮换及时
- [ ] 审计完整
- [ ] 合规通过

## 红牌警告

- 密钥泄露
- 轮换延迟
- 审计缺失
- 权限过大
