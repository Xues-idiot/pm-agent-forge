# 多语言支持 (Multi-Language Support)

## Overview

多语言支持是处理多语言播客内容的技能。包括语言检测、翻译、跨语言搜索等。

## 何时使用

- 多语言播客
- 国际内容
- 翻译需求
- 跨语言研究
- 本地化需求

## 流程

1. **语言检测**：检测音频语言
2. **语言分段**：分段不同语言
3. **分别转录**：分语言转录
4. **翻译处理**：翻译目标语言
5. **术语统一**：统一专业术语
6. **质量校验**：校验翻译质量
7. **多语言索引**：构建多语言索引

## 模板

### 多语言支持模板
```python
class MultiLanguageSupport:
    def __init__(self):
        self.language_detector = LanguageDetector()
        self.translator = Translator()
        self.glossary = TermGlossary()

    async def process_episode(self, audio_path: str, target_lang: str = "zh"):
        """处理多语言剧集"""
        # 1. 语言检测
        segments = await self.language_detector.detect_segments(audio_path)

        # 2. 分语言转录
        transcriptions = {}
        for segment in segments:
            transcript = await self.transcribe(
                audio_path,
                language=segment.language,
                start=segment.start,
                end=segment.end
            )
            transcriptions[segment.id] = transcript

        # 3. 翻译
        translations = {}
        for seg_id, text in transcriptions.items():
            # 应用术语表
            text = self.glossary.apply(text, target_lang)
            # 翻译
            translated = await self.translator.translate(text, target_lang)
            translations[seg_id] = translated

        # 4. 合并结果
        return MultiLanguageEpisode(
            original=transcriptions,
            translated=translations,
            language_distribution=self.analyze_distribution(segments)
        )

    async def cross_language_search(self, query: str, lang: str):
        """跨语言搜索"""
        query_emb = await self.get_embedding(query, lang)
        # 搜索所有语言
        results = await self.vector_store.search_multilingual(query_emb)
        return self.filter_by_language(results, lang)
```

## 检查清单

- [ ] 检测准确
- [ ] 转录正确
- [ ] 翻译流畅
- [ ] 术语一致

## 红牌警告

- 检测错误
- 转录失败
- 翻译生硬
- 术语混乱
