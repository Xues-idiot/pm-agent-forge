# Skills审计 (Skills Audit)

## Overview

Skills审计是审计和优化Skills质量的技能。包括规范性检查、重复检测、质量评估、改进建议等。

## 何时使用

- 定期审计
- 新增审查
- 质量提升
- 重复合并
- 规范化

## 流程

1. **收集信息**：收集Skills信息
2. **规范性检查**：检查SKILL.md规范
3. **重复检测**：检测重复Skills
4. **质量评估**：评估质量
5. **改进建议**：给出改进建议
6. **合并优化**：合并优化重复
7. **报告输出**：输出审计报告

## 模板

### Skills审计模板
```python
class SkillsAudit:
    async def audit_all_skills(self):
        """审计所有Skills"""
        skills = await self.get_all_skills()
        results = {
            "规范性": await self.check_standards(skills),
            "重复性": await self.check_duplicates(skills),
            "完整性": await self.check_completeness(skills),
            "质量": await self.assess_quality(skills)
        }
        return {
            "total_skills": len(skills),
            "issues": self.summarize_issues(results),
            "recommendations": self.generate_recommendations(results)
        }

    async def check_standards(self, skills: List[Skill]):
        """检查规范性"""
        issues = []
        for skill in skills:
            checks = {
                "has_overview": bool(skill.overview),
                "has_template": bool(skill.template),
                "has_checklist": bool(skill.checklist),
                "has_red_flags": bool(skill.red_flags),
                "template_quality": self.check_template_quality(skill)
            }
            if not all(checks.values()):
                issues.append({"skill": skill.name, "issues": checks})
        return issues

    async def find_duplicates(self, skills: List[Skill]):
        """检测重复"""
        duplicates = []
        for i, s1 in enumerate(skills):
            for s2 in skills[i+1:]:
                similarity = self.calculate_similarity(s1, s2)
                if similarity > 0.8:
                    duplicates.append({"skill1": s1.name, "skill2": s2.name, "similarity": similarity})
        return duplicates
```

## 检查清单

- [ ] 格式规范
- [ ] 无重复
- [ ] 内容完整
- [ ] 质量达标
- [ ] 文档同步

## 红牌警告

- 格式不规范
- 存在重复
- 内容缺失
- 质量不达标
