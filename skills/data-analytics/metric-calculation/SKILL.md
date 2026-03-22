---
name: data-analytics-metric-calculation
description: Use when calculating business metrics, KPIs, computing aggregations, or defining measurement formulas.
---

# Data Analytics Metric Calculation Skill

计算业务指标和 KPI，确保数据度量的准确性。

## 何时使用

- 需要计算业务指标
- 定义新的 KPI
- 验证数据计算逻辑
- 设计数据监控体系
- 搭建指标看板

## 指标计算流程

```
1. 理解业务需求 → 2. 定义指标 → 3. 明确口径 → 4. 编写公式 → 5. 验证结果 → 6. 文档化
```

### 1. 理解业务需求

**业务问题：**
```markdown
## 业务问题

### 核心问题
[要解决什么业务问题]

### 业务场景
[在什么场景下使用]

### 使用频率
- [ ] 实时监控
- [ ] 每日汇总
- [ ] 每周/每月报表
```

### 2. 定义指标

**指标分类：**

| 分类维度 | 类型 | 示例 |
|---------|------|------|
| 按业务 | 用户指标 | DAU、MAU、新增 |
| 按业务 | 交易指标 | GMV、订单数、客单价 |
| 按业务 | 转化指标 | 转化率、留存率 |
| 按业务 | 质量指标 | 满意度、NPS |
| 按计算 | 基础指标 | 可直接计算 |
| 按计算 | 衍生指标 | 基于基础指标计算 |
| 按时效 | 实时指标 | 当前在线人数 |
| 按时效 | T+1 指标 | 隔日汇总 |

### 3. 明确口径

**指标口径定义：**

```markdown
## 指标口径

### 基础指标
| 指标名称 | 计算公式 | 说明 |
|---------|---------|------|
| DAU | COUNT(DISTINCT user_id) | 日活用户数 |
| 新增用户 | COUNT(DISTINCT user_id) WHERE first_login = date | 当日新注册用户 |

### 衍生指标
| 指标名称 | 计算公式 | 说明 |
|---------|---------|------|
| 转化率 | 付费用户数 / DAU × 100% | 付费转化比例 |
| 客单价 | GMV / 订单数 | 每单平均金额 |
| ARPU | GMV / 活跃用户数 | 每用户平均收入 |

### 统计口径
- **去重口径**：基于什么字段去重
- **时间口径**：按照什么时间计算（自然日/任意一天）
- **用户口径**：包含哪些用户
- **行为口径**：满足什么条件算
```

### 4. 编写公式

**SQL 实现模板：**

```sql
-- DAU（日活跃用户）
SELECT
    dt AS 日期,
    COUNT(DISTINCT user_id) AS dau
FROM dwd_user_action
WHERE dt = '${bizdate}'
GROUP BY dt;

-- 新增用户
SELECT
    dt AS 日期,
    COUNT(DISTINCT user_id) AS new_users
FROM dwd_user_first_login
WHERE dt = '${bizdate}'
GROUP BY dt;

-- 转化率
SELECT
    dt AS 日期,
    COUNT(DISTINCT CASE WHEN has_paid = 1 THEN user_id END) AS paid_users,
    COUNT(DISTINCT user_id) AS total_users,
    COUNT(DISTINCT CASE WHEN has_paid = 1 THEN user_id END) * 100.0 /
        COUNT(DISTINCT user_id) AS conversion_rate
FROM dwd_user_action
WHERE dt = '${bizdate}'
GROUP BY dt;

-- 留存率（次日留存）
SELECT
    dt AS 注册日期,
    COUNT(DISTINCT user_id) AS day0_users,
    COUNT(DISTINCT CASE WHEN retention_day = 1 THEN user_id END) AS day1_users,
    COUNT(DISTINCT CASE WHEN retention_day = 1 THEN user_id END) * 100.0 /
        COUNT(DISTINCT user_id) AS day1_retention
FROM (
    SELECT
        a.user_id,
        a.dt,
        DATEDIFF(b.dt, a.dt) AS retention_day
    FROM dwd_user_first_login a
    LEFT JOIN dwd_user_action b ON a.user_id = b.user_id AND DATEDIFF(b.dt, a.dt) = 1
    WHERE a.dt BETWEEN '${start_date}' AND '${end_date}'
) t
GROUP BY dt;
```

**Python 实现模板：**

```python
import pandas as pd

def calculate_dau(df):
    """计算 DAU"""
    return df.groupby('dt')['user_id'].nunique()

def calculate_retention(df, login_df, n_days=1):
    """计算 N 日留存率"""
    # 获取首次登录
    first_login = login_df.groupby('user_id')['dt'].min().reset_index()
    first_login.columns = ['user_id', 'first_login']

    # 获取第 N 天登录
    df_with_first = df.merge(first_login, on='user_id')
    df_with_first['days_since_first'] = (
        pd.to_datetime(df_with_first['dt']) -
        pd.to_datetime(df_with_first['first_login'])
    ).dt.days

    # 计算留存
    total_users = len(first_login)
    retained_users = df_with_first[df_with_first['days_since_first'] == n_days]['user_id'].nunique()

    return retained_users / total_users * 100 if total_users > 0 else 0
```

### 5. 验证结果

**验证方法：**

```markdown
## 指标验证

### 逻辑验证
- [ ] 计算结果为合理范围
- [ ] 与历史数据趋势一致
- [ ] 各指标间逻辑关系正确

### 数据验证
- [ ] 分子分母数据存在
- [ ] 无除零错误
- [ ] 边界条件处理正确

### 对账验证
- [ ] 与其他数据源对账
- [ ] 与业务系统对账
- [ ] 与财务数据对账（如涉及）
```

**常见问题排查：**

| 问题 | 可能原因 | 排查方法 |
|------|---------|---------|
| 转化率 > 100% | 分子分母口径不一致 | 统一用户口径 |
| 留存率 > 100% | 重复计算 | 检查去重逻辑 |
| 数据为负 | 日期相减方向错误 | 检查日期计算 |
| 数据突增/突降 | 数据延迟或异常 | 检查数据完整性 |

### 6. 文档化

**指标文档模板：**

```markdown
## 指标文档：[指标名称]

### 基本信息
| 属性 | 内容 |
|------|------|
| 指标名称 | |
| 指标英文名 | |
| 指标分类 | |
| 负责人 | |
| 创建日期 | |

### 技术口径
```sql
-- 计算SQL
```

### 业务定义
[业务上如何理解这个指标]

### 使用场景
- 场景1
- 场景2

### 相关指标
- 相关指标1
- 相关指标2

### 更新频率
- [ ] 实时
- [ ] 每日
- [ ] 每周
- [ ] 每月

### 历史趋势
[简要描述历史趋势]
```

## 常用业务指标公式

### 用户指标

| 指标 | 公式 | 说明 |
|------|------|------|
| DAU | COUNT(DISTINCT user_id) WHERE dt = X | 日活跃 |
| MAU | COUNT(DISTINCT user_id) WHERE dt BETWEEN X AND Y | 月活跃 |
| 新增用户 | COUNT(DISTINCT user_id) WHERE first_login = X | 日新增 |
| 活跃率 | DAU / 累计用户数 | 活跃占比 |

### 转化指标

| 指标 | 公式 | 说明 |
|------|------|------|
| 转化率 | 转化用户数 / 曝光用户数 × 100% | 整体转化 |
| 点击率 | 点击数 / 曝光数 × 100% | CTR |
| 注册转化 | 注册用户数 / 访问用户数 × 100% | 注册转化 |

### 留存指标

| 指标 | 公式 | 说明 |
|------|------|------|
| 次日留存 | D+1回访用户 / D+0新增用户 × 100% | 短期留存 |
| 7日留存 | D+7回访用户 / D+0新增用户 × 100% | 中期留存 |
| 30日留存 | D+30回访用户 / D+0新增用户 × 100% | 长期留存 |

### 收入指标

| 指标 | 公式 | 说明 |
|------|------|------|
| GMV | SUM(order_amount) | 商品交易总额 |
| 客单价 | GMV / 订单数 | 平均订单金额 |
| ARPU | GMV / 活跃用户数 | 每用户收入 |
| ARPPU | GMV / 付费用户数 | 每付费用户收入 |
| 付费率 | 付费用户数 / 活跃用户数 × 100% | 付费比例 |

### 效率指标

| 指标 | 公式 | 说明 |
|------|------|------|
| 人均时长 | 总使用时长 / 活跃用户数 | 用户投入 |
| 人均次数 | 总使用次数 / 活跃用户数 | 使用频率 |
| 复购率 | 购买2次+用户数 / 总购买用户数 × 100% | 重复购买 |

## 指标计算检查清单

- [ ] 业务需求理解准确
- [ ] 指标定义清晰
- [ ] 计算口径明确
- [ ] SQL/Python 实现正确
- [ ] 边界条件处理
- [ ] 结果验证通过
- [ ] 文档记录完整

## 红牌警告

- 口径定义模糊导致歧义
- 分子分母不匹配
- 忽略去重逻辑
- 时间时区混乱
- 缺少边界条件处理
- 多数据源结果不一致
- 指标定义经常变更
