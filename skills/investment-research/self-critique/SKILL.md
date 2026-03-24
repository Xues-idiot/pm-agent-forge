# Agent自批评机制 (Self-Critique Mechanism)

## Overview

Agent自批评机制是让投研Agent具备自我审视和纠错能力的技能。参考investment-thesis-agent的Critic Agent设计，实现多阶段推理循环。

## 何时使用

- 防止幻觉和错误
- 提高研报质量
- 识别逻辑漏洞
- 交叉验证结论

## 流程

1. **初稿生成**：Agent生成初稿分析
2. **批评审查**：Critic Agent审查初稿
3. **问题识别**：识别问题点
4. **修订完善**：Agent根据批评修订
5. **再次审查**：Critic再次审查
6. **迭代优化**：重复直到达标
7. **最终输出**：输出最终版本

## 模板

### 自批评流程模板
```python
# 自批评Agent定义
CRITIC_PROMPT = """你是一位资深投资分析师，负责审查投研报告。

审查维度：
1. 事实准确性 - 数据是否准确？
2. 逻辑严密性 - 推理是否合理？
3. 风险揭示 - 风险是否充分？
4. 投资建议 - 建议是否可执行？
5. 一致性 - 结论与数据是否一致？

请识别：
- 事实错误
- 逻辑漏洞
- 缺失的风险因素
- 过于乐观的假设
- 前后矛盾之处

输出格式：
{
    "issues": [{"severity": "high/medium/low", "description": "...", "suggestion": "..."}],
    "overall_assessment": "...",
    "recommendation": "revision_needed/approved"
}
"""

def self_critique_loop(state: ResearchState, max_iterations: int = 3) -> ResearchState:
    for i in range(max_iterations):
        # 生成/修订报告
        draft = generate_draft(state)

        # Critic审查
        critique = critic_agent.review(draft)

        if critique["recommendation"] == "approved":
            return {"report": draft, "iterations": i + 1}

        # 根据批评修订
        state["feedback"] = critique["issues"]
        draft = revise_draft(draft, critique["issues"])

    return {"report": draft, "iterations": max_iterations}
```

## 检查清单

- [ ] 批评维度全面
- [ ] 问题识别准确
- [ ] 修订有效
- [ ] 迭代控制合理
- [ ] 最终质量达标
- [ ] 效率可接受

## 红牌警告

- 批评流于形式
- 问题识别不准确
- 修订无效
- 迭代过多效率低
- 批评标准不一致
