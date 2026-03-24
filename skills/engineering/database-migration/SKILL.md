# 数据库迁移 (Database Migration)

## Overview

数据库迁移是进行数据库版本管理和数据迁移的技能。包括迁移脚本、灰度迁移、回滚策略、数据校验等。

## 何时使用

- 数据库升级
- 表结构变更
- 数据清洗
- 分库分表
- 数据库切换

## 流程

1. **现状分析**：分析当前数据库
2. **迁移设计**：设计迁移方案
3. **脚本编写**：编写迁移脚本
4. **灰度执行**：灰度执行迁移
5. **数据校验**：校验数据一致性
6. **回滚准备**：准备回滚方案
7. **全量执行**：执行全量迁移

## 模板

### 数据库迁移模板
```python
class DatabaseMigration:
    async def plan_migration(self, source: DB, target: DB):
        """规划迁移"""
        # 分析差异
        diff = await self.analyze_diff(source, target)
        # 评估风险
        risk = self.assess_risk(diff)
        # 生成方案
        return {
            "steps": self.generate_steps(diff),
            "risk_level": risk,
            "rollback_plan": self.generate_rollback(diff),
            "verification": self.generate_verification(diff)
        }

    async def execute_migration(self, plan: MigrationPlan):
        """执行迁移"""
        # 创建备份
        await self.create_backup()

        # 生成临时表
        await self.create_staging_table()

        # 灰度迁移
        for batch in self.batch_migrate(plan.data, 1000):
            await self.migrate_batch(batch)
            await self.verify_batch(batch)

        # 切换流量
        await self.switch_traffic()

        # 验证
        await self.final_verification()

    async def rollback(self):
        """回滚"""
        await self.restore_from_backup()
        await self.switch_to_original()
```

## 检查清单

- [ ] 备份完整
- [ ] 脚本正确
- [ ] 灰度执行
- [ ] 数据一致
- [ ] 回滚方案

## 红牌警告

- 备份失败
- 脚本错误
- 数据丢失
- 校验失败
- 回滚失效
