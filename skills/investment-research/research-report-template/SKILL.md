# 研究报告模板库 (Research Report Templates)

## Overview

投研报告模板库是提供标准化研报模板的技能。参考AiBuffett的报告格式，设计专业研报模板。

## 何时使用

- 生成标准研报
- 保证报告质量
- 提升效率
- 风格统一

## 流程

1. **模板设计**：设计模板结构
2. **内容规范**：规范各章节内容
3. **格式定义**：定义格式标准
4. **变量定义**：定义动态变量
5. **生成开发**：开发生成器
6. **测试验证**：验证模板效果
7. **持续优化**：根据反馈优化

## 模板

### 标准研报模板
```markdown
# [公司名称] 投资价值研究报告

**评级**: {{rating}} | **目标价**: {{target_price}}元 | **当前价**: {{current_price}}元
**潜在涨幅**: {{upside}}% | **分析师**: {{analyst}} | **日期**: {{date}}

---

## 执行摘要

{{executive_summary}}

## 投资亮点
{{investment_highlights}}

## 风险提示
{{risk_warnings}}

---

## 1. 公司概况

### 1.1 基本信息
- 股票代码: {{stock_code}}
- 所属行业: {{industry}}
- 主营业务: {{main_business}}

### 1.2 投资逻辑
{{investment_thesis}}

## 2. 行业分析

### 2.1 行业规模
{{industry_size}}

### 2.2 竞争格局
{{competitive_landscape}}

### 2.3 发展趋势
{{industry_trends}}

## 3. 财务分析

### 3.1 核心财务指标
| 指标 | {{year1}} | {{year2}} | {{year3}} | 行业均值 |
|------|-----------|-----------|-----------|----------|
| 营收(亿) | {{revenue1}} | {{revenue2}} | {{revenue3}} | {{ind_avg}} |
| 净利润(亿) | {{profit1}} | {{profit2}} | {{profit3}} | - |
| 毛利率 | {{margin1}}% | {{margin2}}% | {{margin3}}% | {{ind_margin}}% |
| ROE | {{roe1}}% | {{roe2}}% | {{roe3}}% | {{ind_roe}}% |

### 3.2 财务质量评估
{{financial_quality}}

## 4. 估值分析

### 4.1 估值方法对比
| 方法 | 估值 | 对应股价 | 逻辑 |
|------|------|----------|------|
| PE | {{pe_value}} | {{pe_price}} | {{pe_logic}} |
| PB | {{pb_value}} | {{pb_price}} | {{pb_logic}} |
| DCF | {{dcf_value}} | {{dcf_price}} | {{dcf_logic}} |

### 4.2 综合估值
{{comprehensive_valuation}}

## 5. 投资建议

### 5.1 评级与目标价
- **评级**: {{rating}}
- **目标价**: {{target_price}}元
- **当前价**: {{current_price}}元
- **潜在涨幅**: {{upside}}%

### 5.2 核心逻辑
{{core_rationale}}

### 5.3 风险因素
{{risk_factors}}

---
*本报告仅供参考，不构成投资建议*
```

## 检查清单

- [ ] 结构完整
- [ ] 内容规范
- [ ] 格式统一
- [ ] 变量完整
- [ ] 生成高效
- [ ] 易于维护

## 红牌警告

- 结构混乱
- 内容缺失
- 格式不统一
- 变量不完整
- 生成效率低
