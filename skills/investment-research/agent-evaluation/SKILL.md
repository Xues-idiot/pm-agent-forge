# Agent效果评估 (Agent Evaluation)

## Overview

Agent效果评估是评估投研Agent输出质量的技能。建立评估体系，持续优化Agent表现。

## 何时使用

- 评估Agent输出质量
- 对比不同Agent版本
- 优化Agent性能
- 构建评估基准

## 流程

1. **指标设计**：设计评估指标
2. **数据集构建**：构建测试数据集
3. **评估执行**：执行评估
4. **结果分析**：分析评估结果
5. **问题定位**：定位问题
6. **优化实施**：优化Agent
7. **复评验证**：验证优化效果

## 模板

### 评估指标模板
```python
EVALUATION_METRICS = {
    # 准确性指标
    "accuracy": {
        "financial_data_accuracy": "财务数据准确性",
        "valuation_accuracy": "估值准确性",
        "forecast_accuracy": "预测准确性",
    },

    # 完整性指标
    "completeness": {
        "dimension_coverage": "分析维度覆盖率",
        "risk_disclosure": "风险揭示完整度",
        "data_support": "数据支撑完整度",
    },

    # 及时性指标
    "timeliness": {
        "response_time": "响应时间",
        "data_freshness": "数据新鲜度",
    },

    # 可用性指标
    "usability": {
        "report_readability": "报告可读性",
        "actionability": "建议可操作性",
    }
}

# 评估示例
def evaluate_agent_output(output, ground_truth):
    scores = {
        "accuracy": calculate_accuracy(output, ground_truth),
        "completeness": calculate_completeness(output),
        "timeliness": calculate_timeliness(output),
        "usability": calculate_usability(output),
    }
    return scores
```

## 检查清单

- [ ] 指标设计合理
- [ ] 数据集有代表性
- [ ] 评估客观公正
- [ ] 问题定位准确
- [ ] 优化有效
- [ ] 复评验证

## 红牌警告

- 指标过于主观
- 数据集偏差
- 评估不公正
- 问题定位错误
- 优化无效
