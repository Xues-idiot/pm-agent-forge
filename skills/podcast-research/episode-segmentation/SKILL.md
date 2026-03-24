# Episode分段处理 (Episode Segmentation)

## Overview

Episode分段处理是将播客内容智能分段处理的技能。包括话题分段、章节分割、关键片段标记等。

## 何时使用

- 长音频处理
- 话题分割
- 内容导航
- 快速预览
- 精准定位

## 流程

1. **音频分析**：分析音频特征
2. **转录处理**：获取文本内容
3. **话题检测**：检测话题边界
4. **分段标记**：标记段落边界
5. **章节生成**：生成章节标题
6. **时间戳校准**：校准时间戳
7. **索引构建**：构建内容索引

## 模板

### 播客分段模板
```python
class PodcastSegmenter:
    def __init__(self):
        self.speaker_diarizer = SpeakerDiarizer()
        self.topic_detector = TopicDetector()
        self.silence_detector = SilenceDetector()

    async def segment_episode(self, audio_path: str):
        """分割Episode"""
        # 1. 转录
        transcript = await self.transcribe(audio_path)

        # 2. 说话人分离
        speakers = await self.speaker_diarizer.process(audio_path)

        # 3. 话题分段
        segments = await self.topic_detector.detect(transcript)

        # 4. 静音检测辅助分段
        silence_boundaries = await self.silence_detector.find(audio_path)

        # 5. 合并分段
        final_segments = self.merge_segments(segments, silence_boundaries)

        # 6. 生成章节标题
        for segment in final_segments:
            segment.title = await self.generate_title(segment.text)

        return EpisodeSegments(
            segments=final_segments,
            speakers=speakers,
            duration=self.get_duration(audio_path)
        )

    async def generate_title(self, text: str) -> str:
        """生成章节标题"""
        summary = await self.summarize(text, max_length=50)
        return summary
```

## 检查清单

- [ ] 转录准确
- [ ] 分段合理
- [ ] 标题贴切
- [ ] 时间戳准确
- [ ] 索引完整

## 红牌警告

- 分段错误
- 标题偏差
- 时间戳漂移
- 遗漏重要内容
