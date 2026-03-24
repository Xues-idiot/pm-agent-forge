# 思维导图生成 (Mind Map Generation)

## Overview

思维导图生成是将播客内容转换为可视化思维导图的技能。

## 何时使用

- 可视化内容结构
- 整理要点关系
- 学习笔记
- 分享展示

## 流程

1. **内容分析**：分析内容结构
2. **主题提取**：提取核心主题
3. **关系识别**：识别主题关系
4. **层级设计**：设计导图层级
5. **节点生成**：生成导图节点
6. **可视化**：生成思维导图
7. **导出分享**：导出多种格式

## 模板

### 思维导图生成
```python
from markmap import MarkdownMatter

async def generate_mindmap(transcription: Transcription) -> str:
    """生成思维导图"""
    # 提取主题和要点
    topics = extract_topics(transcription.text)
    points = extract_key_points(transcription.text)

    # 生成Markdown格式
    markdown = f"""# {transcription.title}

## 核心主题
{format_as_mindmap(topics)}

## 关键要点
{format_as_mindmap(points)}

## 详细内容
{format_as_mindmap(detailed_points)}
"""

    # 生成思维导图HTML
    html = markmap.Markmap.from_markdown(markdown)
    return html

def format_as_mindmap(items: List[str], level: int = 2) -> str:
    """格式化思维导图"""
    lines = []
    for item in items:
        lines.append(f"{'#' * level} {item}")
    return "\n".join(lines)
```

## 检查清单

- [ ] 结构清晰
- [ ] 要点完整
- [ ] 层级合理
- [ ] 可视化美观
- [ ] 交互友好
- [ ] 导出格式

## 红牌警告

- 结构混乱
- 要点遗漏
- 层级过深
- 界面不友好
- 导出失败
