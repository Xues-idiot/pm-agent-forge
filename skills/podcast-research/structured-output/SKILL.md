# 结构化输出 (Structured Output)

## Overview

结构化输出是将播客内容输出为JSON/Markdown/Notion等结构化格式的技能。

## 何时使用

- 数据导出
- 系统集成
- 笔记整理
- 格式转换

## 流程

1. **内容分析**：分析输出需求
2. **结构设计**：设计输出结构
3. **内容映射**：映射内容到结构
4. **格式化**：格式化输出
5. **校验**：校验输出
6. **导出**：导出目标格式
7. **同步**：同步到目标平台

## 模板

### 支持的输出格式
```python
OUTPUT_FORMATS = {
    "json": {
        "schema": "podcast_schema.json",
        "indent": 2
    },
    "markdown": {
        "template": "podcast_template.md",
        "toc": True
    },
    "notion": {
        "database_id": "xxx",
        "properties_mapping": {}
    },
    "obsidian": {
        "vault_path": "path/to/vault",
        "frontmatter": True,
        "links": "wiki"
    }
}

async def export_episode(episode: Episode, format: str) -> ExportedContent:
    """导出Episode"""
    if format == "json":
        return export_as_json(episode)
    elif format == "markdown":
        return export_as_markdown(episode)
    elif format == "notion":
        return await export_to_notion(episode)
    elif format == "obsidian":
        return await export_to_obsidian(episode)
```

## 检查清单

- [ ] 结构完整
- [ ] 内容准确
- [ ] 格式规范
- [ ] 校验通过
- [ ] 导出成功
- [ ] 同步正确

## 红牌警告

- 结构不完整
- 内容缺失
- 格式错误
- 校验失败
- 导出失败
- 同步失败
