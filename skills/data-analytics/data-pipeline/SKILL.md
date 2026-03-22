---
name: data-analytics-data-pipeline
description: Use when designing data pipelines, building ETL processes, or managing data integration workflows.
---

# Data Pipeline Design Skill

设计数据流水线，构建ETL流程，管理数据集成工作流。

## 何时使用

- 数据流水线设计
- ETL流程构建
- 数据同步
- 实时数据处理
- 数据质量保障
- 调度系统设计

## 数据流水线流程

```
1. 需求分析 → 2. 架构设计 → 3. 开发实现 → 4. 质量保障 → 5. 运维监控
```

### 1. 需求分析

**数据源盘点：**

```markdown
## 数据源盘点

### 数据源类型
| 类型 | 示例 | 数据量 | 同步频率 |
|------|------|--------|----------|
| 业务数据库 | MySQL/Oracle | 大 | 实时/准实时 |
| 日志系统 | Nginx/Kafka | 大 | 准实时 |
| 第三方API | 天气/地图 | 中 | 批量 |
| 文件系统 | CSV/JSON | 不等 | 批量 |

### 源系统评估
| 系统 | 数据质量 | 接口稳定性 | 支持程度 |
|------|----------|------------|----------|
| | | | |
```
```

**数据需求：**

```markdown
## 数据需求

### 业务需求
- [ ] 报表数据需求
- [ ] 实时大屏需求
- [ ] 算法特征需求
- [ ] 审计数据需求

### 性能需求
| 需求类型 | 要求 |
|----------|------|
| 数据延迟 | 准实时<5分钟 / 批量<T+1 |
| 数据准确性 | >99.9% |
| 系统可用性 | >99.9% |
```

### 2. 架构设计

**架构选型：**

```markdown
## 架构选型

### 批处理架构
```markdown
## 批处理架构

数据源 → 数据采集 → 消息队列 → 批处理 → 数据仓库
                         ↓
                      存储层
```

### 流处理架构
```markdown
## 流处理架构

数据源 → 数据采集 → Kafka → 流处理引擎 → 实时库
                              ↓
                           数据仓库
```

### Lambda架构
```markdown
## Lambda架构

              → 批处理层 →
数据源 → 服务层 →             → 合并结果
              → 流处理层 →
```

### Kappa架构
```markdown
## Kappa架构

数据源 → Kafka → 流处理引擎 → 数据仓库
```
```

**技术选型：**

```markdown
## 技术选型

### 数据采集
| 工具 | 适用场景 | 优点 | 缺点 |
|------|----------|------|------|
| DataX | 离线批量 | 支持广 | 实时差 |
| Canal | MySQL同步 | 实时 | 只支持MySQL |
| Debezium | 变更捕获 | 通用 | 复杂度高 |
| Flume | 日志采集 | 专用 | 场景局限 |

### 消息队列
| 工具 | 吞吐量 | 延迟 | 适用场景 |
|------|--------|------|----------|
| Kafka | 高 | 低 | 大数据场景 |
| RabbitMQ | 中 | 低 | 通用场景 |
| RocketMQ | 高 | 低 | 电商场景 |

### 处理引擎
| 工具 | 类型 | 适用场景 |
|------|------|----------|
| Spark | 批+流 | 通用 |
| Flink | 流 | 实时 |
| Hive | 批 | 离线 |
```

### 3. 开发实现

**ETL开发规范：**

```markdown
## ETL开发规范

### 命名规范
```sql
-- 表命名
dwd_业务_主题_类型
dwd_order_info_d  -- 订单信息表（每日全量）

-- 字段命名
- 小写+下划线
- 必须有更新时间字段
- 必须有数据来源字段
```

### 开发模板
```sql
-- ETL模板
INSERT OVERWRITE TABLE {target_table}
SELECT
    -- 必要的字段
    id,
    name,
    -- 维度退化
    dt AS part_date,
    -- 数据来源
    'ods_table' AS src_table,
    -- 时间戳
    CURRENT_TIMESTAMP() AS etl_time
FROM {source_table}
WHERE dt = '{date}'
```

### 异常处理
```sql
-- 数据校验
WHERE 1=1
AND id IS NOT NULL
AND dt = '{date}'
-- 边界校验
AND amount >= 0
```
```

**数据同步：**

```markdown
## 数据同步

### 全量同步
```sql
-- 全量同步策略
TRUNCATE TABLE {target_table};
INSERT INTO {target_table}
SELECT * FROM {source_table};
```

### 增量同步
```sql
-- 基于时间戳
INSERT INTO {target_table}
SELECT * FROM {source_table}
WHERE update_time > (SELECT MAX(update_time) FROM {target_table});

-- 基于CDC
-- 使用binlog/CDC工具同步变更
```

### 拉链历史
```markdown
## 拉链历史表

| 字段 | 说明 |
|------|------|
| start_date | 有效期开始 |
| end_date | 有效期结束 |
| is_current | 是否当前 |

-- 关闭历史
UPDATE table
SET end_date = '2024-01-01',
    is_current = 'N'
WHERE id = {id}
AND is_current = 'Y';
```
```

### 4. 质量保障

**数据质量检查：**

```markdown
## 数据质量检查

### 准确性
| 检查项 | 方法 |
|--------|------|
| 数据记录数 | COUNT对比 |
| 数值字段 | SUM/AVG对比 |
| 枚举字段 | VALUE_SET对比 |

### 完整性
| 检查项 | SQL |
|--------|-----|
| 空值检查 | COUNT(*) WHERE col IS NULL |
| 主键唯一 | GROUP BY + HAVING COUNT>1 |
| 引用完整性 | LEFT JOIN检查 |

### 及时性
```markdown
## 延迟监控

| 任务 | 预期延迟 | 告警阈值 |
|------|----------|----------|
| ODS→DWD | <30分钟 | >1小时 |
| DWD→DWS | <1小时 | >2小时 |
| 全量同步 | <3小时 | >5小时 |
```
```

**质量监控：**

```markdown
## 质量监控

### 告警规则
| 规则 | 条件 | 动作 |
|------|------|------|
| 数据量异常 | 较昨日波动>30% | 告警+阻塞 |
| 空值率异常 | 空值率>10% | 告警 |
| 重复率异常 | 重复率>1% | 告警+阻塞 |

### 质量报告
```markdown
## 每日质量报告

| 表名 | 记录数 | 空值率 | 重复率 | 评分 |
|------|--------|--------|--------|------|
| dwd_order | | | | A |
```
```

### 5. 运维监控

**调度设计：**

```markdown
## 调度设计

### 调度依赖
```markdown
## DAG设计

ods_order → dwd_order → dws_order → ads_business
     ↓
ods_product → dwd_product → dws_product
     ↓
ods_user → dwd_user → dws_user
```

### 调度配置
| 任务 | 调度周期 | 运行时长 | 依赖 |
|------|----------|----------|------|
| 全量同步 | 每日 | 2h | - |
| 增量同步 | 每小时 | 10min | 全量完成 |
| 数据清洗 | 每日 | 1h | 增量完成 |
```

**故障处理：**

```markdown
## 故障处理

### 故障等级
| 等级 | 影响 | 响应时间 | 处理方式 |
|------|------|----------|----------|
| P0 | 数据严重延迟/错误 | 15分钟 | 立即处理 |
| P1 | 小范围数据问题 | 1小时 | 快速修复 |
| P2 | 非核心问题 | 4小时 | 计划修复 |

### 回滚机制
- [ ] 数据回滚脚本
- [ ] 任务重跑机制
- [ ] 降级策略
```

## 数据流水线检查清单

- [ ] 需求分析完整
- [ ] 架构设计合理
- [ ] 开发规范执行
- [ ] 质量保障到位
- [ ] 监控告警完善
- [ ] 故障处理预案
- [ ] 文档记录完整
- [ ] 交接文档齐全

## 红牌警告

- 数据丢失
- 数据重复
- 数据错误
- 调度失败
- 告警失效
- 核心任务阻塞
- 系统资源耗尽
- 敏感数据泄露
