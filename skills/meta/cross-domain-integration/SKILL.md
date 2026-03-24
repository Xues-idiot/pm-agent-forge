# 跨领域整合 (Cross-Domain Integration)

## Overview

跨领域整合是整合多个领域Skills的技能。包括领域映射、流程衔接、数据共享、协同工作等。

## 何时使用

- 多领域协作
- 流程整合
- 数据打通
- 能力组合
- 方案设计

## 流程

1. **领域分析**：分析涉及的领域
2. **能力映射**：映射各领域能力
3. **流程设计**：设计跨域流程
4. **数据整合**：整合数据格式
5. **接口设计**：设计接口
6. **协同机制**：建立协同机制
7. **测试验证**：测试验证

## 模板

### 跨领域整合模板
```python
class CrossDomainIntegration:
    def analyze_domains(self, task: str):
        """分析涉及的领域"""
        return {
            "primary_domain": "pm",
            "secondary_domains": ["engineering", "data"],
            "required_skills": [
                "prd-writing",
                "api-design",
                "data-modeling"
            ],
            "handoff_points": [
                {"from": "prd-writing", "to": "api-design"},
                {"from": "api-design", "to": "data-modeling"}
            ]
        }

    def design_workflow(self, domains: List[str]):
        """设计跨域工作流"""
        return {
            "phases": [
                {"phase": 1, "domain": "pm", "skills": ["prd-writing"], "output": "prd"},
                {"phase": 2, "domain": "engineering", "skills": ["api-design"], "output": "api_spec"},
                {"phase": 3, "domain": "data", "skills": ["data-modeling"], "output": "schema"}
            ],
            "data_flow": {
                "prd": {"format": "markdown", "shared_with": ["engineering", "data"]},
                "api_spec": {"format": "openapi", "shared_with": ["data"]},
                "schema": {"format": "sql", "shared_with": ["engineering"]}
            }
        }

    async def test_integration(self, workflow: dict):
        """测试整合"""
        return {
            "phase_tests": [
                {"phase": 1, "test": "prd_review"},
                {"phase": 2, "test": "api_contract_test"},
                {"phase": 3, "test": "schema_validation"}
            ],
            "integration_tests": [
                "data_flow_test",
                "end_to_end_test"
            ]
        }
```

## 检查清单

- [ ] 领域覆盖
- [ ] 流程清晰
- [ ] 数据打通
- [ ] 协同顺畅
- [ ] 测试通过

## 红牌警告

- 领域遗漏
- 流程断裂
- 数据孤岛
- 协同困难
