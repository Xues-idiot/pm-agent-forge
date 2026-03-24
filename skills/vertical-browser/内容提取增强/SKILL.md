# 内容提取增强 (Content Extraction Enhanced)

## Overview

内容提取增强是使用AI模型提升网页内容提取质量的技能。

## 何时使用

- 复杂页面提取
- 无结构页面
- 需要语义理解
- 高质量提取

## 流程

1. **页面分析**：分析页面结构
2. **区域识别**：识别主要内容区
3. **语义提取**：使用AI提取内容
4. **结构化**：结构化输出
5. **质量校验**：校验提取质量
6. **后处理**：清洗和格式化
7. **存储输出**：存储或输出

## 模板

### AI内容提取模板
```python
async def extract_with_ai(html: str, url: str) -> ExtractedContent:
    """使用AI提取内容"""
    # 初步提取
    raw_content = extract_main_content(html)

    # 使用LLM分析和提取
    prompt = f"""
从以下网页内容中提取关键信息：

URL: {url}

内容:
{raw_content[:5000]}

提取：
1. 标题
2. 作者
3. 发布日期
4. 正文（保留结构）
5. 关键要点
6. 分类标签

JSON格式输出：
"""
    result = await llm.generate(prompt)

    return parse_extracted_content(result)
```

## 检查清单

- [ ] 提取准确
- [ ] 结构完整
- [ ] 格式正确
- [ ] 质量校验
- [ ] 成本控制
- [ ] 性能达标

## 红牌警告

- 提取不完整
- 语义错误
- 格式混乱
- 成本过高
- 延迟过大
