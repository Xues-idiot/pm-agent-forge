---
name: data-analytics-user-portrait
description: Use when building user portrait systems, developing tag engines, or creating user segmentation for data analytics.
---

# User Portrait Analytics Skill

用户画像分析，支撑数据分析和精准运营。

## 何时使用

- 用户画像数据建设
- 标签数据开发
- 用户分群数据
- 画像指标计算
- 数据资产管理

## 画像建设流程

```
1. 业务需求 → 2. 标签设计 → 3. 数据开发 → 4. 画像构建 → 5. 应用迭代
```

### 1. 业务需求

**需求收集：**

```markdown
## 业务需求

### 常见需求场景
| 场景 | 需要的标签 | 优先级 |
|------|------------|--------|
| 精准营销 | 偏好/行为/价值 | P0 |
| 个性化推荐 | 偏好/特征 | P0 |
| 流失预警 | 活跃度/行为 | P1 |
| 用户洞察 | 人口/行为/价值 | P1 |
| 风控 | 信用/行为异常 | P0 |
```

**需求文档模板：**

```markdown
## 画像需求文档

### 1. 需求背景
[业务背景和目标]

### 2. 标签需求
| 标签名 | 类型 | 定义 | 优先级 |
|--------|------|------|--------|
| | | | |

### 3. 应用场景
[如何使用这些标签]

### 4. 预期效果
[期望达成的目标]
```
```

### 2. 标签设计

**标签分类体系：**

```markdown
## 标签分类

### 属性类标签
| 标签 | 类型 | 数据源 | 更新频率 |
|------|------|--------|----------|
| age | 数值 | 用户注册 | 月度 |
| gender | 枚举 | 用户注册 | 静态 |
| city_level | 枚举 | IP/地址 | 月度 |
| member_level | 枚举 | 会员系统 | 实时 |

### 统计类标签
| 标签 | 类型 | 数据源 | 更新频率 |
|------|------|--------|----------|
| last_7d_order_cnt | 数值 | 订单表 | 每日 |
| last_30d_gmv | 数值 | 订单表 | 每日 |
| avg_order_amount | 数值 | 订单表 | 每日 |

### 规则类标签
| 标签 | 类型 | 规则 | 更新频率 |
|------|------|------|----------|
| vip_level | 枚举 | GMV累计分层 | 每日 |
| is_high_risk | 布尔 | 异常行为规则 | 实时 |
| user_lifecycle | 枚举 | 行为规则 | 每日 |

### 模型类标签
| 标签 | 类型 | 模型 | 更新频率 |
|------|------|------|----------|
| purchase_probability | 数值 | 预测模型 | 每日 |
| churn_probability | 数值 | 流失模型 | 每日 |
| credit_score | 数值 | 信用模型 | 每周 |
```
```

**标签定义模板：**

```markdown
## 标签定义

### 基本信息
- 标签名称：user_gender
- 标签中文名：性别
- 标签类型：枚举
- 标签值：['M','F','U']（男/女/未知）

### 数据规格
- 数据来源：dwd_user_info_d
- 计算逻辑：直接取 gender字段
- 统计周期：无
- 更新频率：实时

### 技术实现
```sql
-- 伪代码
SELECT
    user_id,
    gender as user_gender
FROM dwd_user_info_d
WHERE dt = '${bizdate}'
```
```

### 3. 数据开发

**数据模型设计：**

```markdown
## 数据模型

### 画像表结构
```sql
-- 用户基础画像表
CREATE TABLE dws_user_profile_d (
    user_id STRING COMMENT '用户ID',
    -- 属性标签
    gender STRING COMMENT '性别',
    age INT COMMENT '年龄',
    city_level STRING COMMENT '城市等级',
    -- 统计标签
    last_7d_order_cnt INT COMMENT '近7天订单数',
    last_30d_gmv DECIMAL(12,2) COMMENT '近30天GMV',
    -- 规则标签
    user_level STRING COMMENT '用户等级',
    is_high_value STRING COMMENT '是否高价值',
    -- 模型标签
    purchase_probability DOUBLE COMMENT '购买概率',
    churn_probability DOUBLE COMMENT '流失概率',
    -- 系统字段
    etl_time TIMESTAMP COMMENT '更新时间'
) COMMENT '用户画像表'
PARTITIONED BY (dt STRING);
```
```

**ETL开发规范：**

```markdown
## ETL开发规范

### 开发流程
```markdown
## 开发步骤

1. 需求评审 → 2. 标签设计 → 3. SQL开发 → 4. 测试验证 → 5. 上线发布

### 命名规范
- 表名：dws_user_profile_d
- 字段：小写+下划线
- 分区：dt=YYYYMMDD
```

### 标签计算示例
```sql
-- 性别标签
INSERT OVERWRITE TABLE dws_user_profile_d PARTITION(dt='${bizdate}')
SELECT
    user_id,
    gender,
    -- 统计类：近7天订单数
    COUNT(DISTINCT order_id) as last_7d_order_cnt,
    -- 规则类：是否高价值（近30天消费>1000）
    CASE WHEN SUM(gmv) > 1000 THEN 'Y' ELSE 'N' END as is_high_value
FROM dwd_order_d
WHERE dt BETWEEN '${date_7d_ago}' AND '${bizdate}'
GROUP BY user_id, gender;
```
```

### 4. 画像构建

**用户分群计算：**

```markdown
## 用户分群

### 价值分层
```sql
-- RFM分层
WITH rfm AS (
    SELECT
        user_id,
        DATEDIFF(CURRENT_DATE, MAX(order_date)) as recency,  -- 最近购买
        COUNT(order_id) as frequency,  -- 购买频次
        SUM(gmv) as monetary  -- 消费金额
    FROM dwd_order_d
    WHERE dt = '${bizdate}'
    GROUP BY user_id
)
SELECT
    user_id,
    CASE
        WHEN recency <= 7 AND frequency >= 5 AND monetary >= 1000 THEN '重要价值'
        WHEN recency <= 7 AND frequency >= 3 THEN '重要发展'
        WHEN recency > 30 THEN '重要挽留'
        ELSE '一般用户'
    END as user_segment
FROM rfm;
```
```

**画像宽表构建：**

```markdown
## 画像宽表

### 多源标签整合
```sql
-- 构建用户画像宽表
INSERT OVERWRITE TABLE dws_user_profile_full_d PARTITION(dt='${bizdate}')
SELECT
    u.user_id,
    -- 基础属性（来自用户表）
    u.gender,
    u.age,
    u.city_level,
    -- 行为统计（来自订单表）
    o.last_30d_gmv,
    o.last_30d_order_cnt,
    o.avg_order_amount,
    -- 偏好特征（来自行为表）
    p.prefer_category,
    p.prefer_price_range,
    -- 模型预测（来自模型表）
    m.purchase_probability,
    m.churn_probability,
    -- 计算时间
    CURRENT_TIMESTAMP() as etl_time
FROM dwd_user_info_d u
LEFT JOIN (
    SELECT user_id,
           SUM(gmv) as last_30d_gmv,
           COUNT(order_id) as last_30d_order_cnt,
           AVG(gmv) as avg_order_amount
    FROM dwd_order_d
    WHERE dt BETWEEN '${date_30d_ago}' AND '${bizdate}'
    GROUP BY user_id
) o ON u.user_id = o.user_id
LEFT JOIN (
    SELECT user_id,
           MAX(category) as prefer_category,
           MAX(price_range) as prefer_price_range
    FROM dwd_user_behavior_d
    GROUP BY user_id
) p ON u.user_id = p.user_id
LEFT JOIN (
    SELECT user_id,
           purchase_probability,
           churn_probability
    FROM dws_user_ml_features_d
    WHERE dt = '${bizdate}'
) m ON u.user_id = m.user_id;
```
```

### 5. 应用迭代

**应用场景：**

```markdown
## 画像应用

### 营销应用
```sql
-- 高价值用户精准营销
SELECT user_id, gender, city_level, last_30d_gmv
FROM dws_user_profile_full_d
WHERE is_high_value = 'Y'
  AND churn_probability > 0.5
  AND prefer_category = '美妆';
```
```

**效果追踪：**

```markdown
## 效果追踪

### 标签覆盖率
| 标签 | 覆盖率 | 准确率 | 更新率 |
|------|--------|--------|--------|
| gender | 98% | 95% | 实时 |
| age | 95% | 90% | 月度 |
| user_level | 100% | 99% | 每日 |

### 应用效果
| 应用 | 标签 | 效果指标 |
|------|------|----------|
| 精准推送 | prefer_category | 转化率+15% |
| 流失召回 | churn_probability | 召回率+20% |
```
```

## 用户画像检查清单

- [ ] 业务需求清晰
- [ ] 标签定义明确
- [ ] 数据来源可靠
- [ ] 计算逻辑正确
- [ ] 更新频率合理
- [ ] 覆盖率达标
- [ ] 准确率验证
- [ ] 应用效果追踪

## 红牌警告

- 标签定义不清晰
- 数据源质量差
- 口径不统一
- 更新不及时
- 覆盖率不达标
- 准确率低
- 只建不用
- 隐私不合规
