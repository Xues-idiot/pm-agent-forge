# 投研数据库设计 (Research Database Design)

## Overview

投研数据库设计是为投研系统设计数据存储方案的技能。参考FinSight的SQLite设计，构建高效的数据存储。

## 何时使用

- 历史数据存储
- 实时行情缓存
- 研究报告存储
- 用户数据管理

## 流程

1. **需求分析**：确定数据需求
2. **数据建模**：设计数据模型
3. **库表设计**：设计库表结构
4. **索引设计**：设计索引
5. **缓存设计**：设计缓存策略
6. **迁移方案**：设计迁移方案
7. **运维规范**：制定运维规范

## 模板

### 数据库设计模板
```sql
-- 股票基础信息
CREATE TABLE stocks (
    stock_code VARCHAR(10) PRIMARY KEY,
    stock_name VARCHAR(100) NOT NULL,
    industry VARCHAR(50),
    listing_date DATE,
    market_cap DECIMAL(20, 2),
    INDEX idx_industry (industry)
);

-- 日线行情
CREATE TABLE daily_price (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    stock_code VARCHAR(10),
    trade_date DATE,
    open_price DECIMAL(10, 2),
    high_price DECIMAL(10, 2),
    low_price DECIMAL(10, 2),
    close_price DECIMAL(10, 2),
    volume BIGINT,
    turnover DECIMAL(20, 2),
    UNIQUE KEY uk_stock_date (stock_code, trade_date),
    INDEX idx_trade_date (trade_date)
);

-- 财务数据
CREATE TABLE financial_data (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    stock_code VARCHAR(10),
    report_date DATE,
    revenue DECIMAL(20, 2),
    net_profit DECIMAL(20, 2),
    total_assets DECIMAL(20, 2),
    total_liabilities DECIMAL(20, 2),
    INDEX idx_stock_report (stock_code, report_date)
);

-- 研究报告
CREATE TABLE research_reports (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    stock_code VARCHAR(10),
    title VARCHAR(200),
    content TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    INDEX idx_stock (stock_code)
);
```

## 检查清单

- [ ] 范式设计合理
- [ ] 索引有效
- [ ] 数据完整
- [ ] 性能优化
- [ ] 安全加固
- [ ] 备份策略

## 红牌警告

- 表结构混乱
- 索引缺失
- 数据冗余
- 性能问题
- 安全漏洞
