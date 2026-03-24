# 多语言翻译 (Translation)

## Overview

多语言翻译是将播客内容翻译成多种语言的技能。

## 何时使用

- 跨语言内容传播
- 翻译学习
- 多语言字幕
- 国际传播

## 流程

1. **语言检测**：检测内容语言
2. **翻译准备**：准备翻译内容
3. **翻译执行**：执行翻译
4. **术语统一**：统一专业术语
5. **质量校验**：校验翻译质量
6. **格式输出**：输出翻译结果
7. **字幕生成**：生成翻译字幕

## 模板

### 翻译配置
```python
TRANSLATION_CONFIG = {
    "target_langs": ["en", "ja", "ko", "zh-TW"],
    "preserve_format": True,
    "terminology_glossary": "path/to/glossary.json",
    "quality_check": True
}

async def translate_episode(episode: Episode, target_lang: str) -> TranslatedEpisode:
    """翻译Episode"""
    # 分段翻译
    segments = []
    for seg in episode.transcription.segments:
        translated = await translator.translate(
            seg.text,
            source_lang="zh",
            target_lang=target_lang,
            preserve_format=True
        )
        segments.append(TranslatedSegment(
            original=seg.text,
            translated=translated,
            start=seg.start,
            end=seg.end
        ))

    return TranslatedEpisode(
        original_episode=episode.title,
        language=target_lang,
        segments=segments,
        translator="AI"
    )
```

## 检查清单

- [ ] 语言检测
- [ ] 翻译准确
- [ ] 术语统一
- [ ] 格式保留
- [ ] 质量校验
- [ ] 字幕同步

## 红牌警告

- 翻译不准确
- 术语混乱
- 格式丢失
- 时间戳错位
- 文化差异
