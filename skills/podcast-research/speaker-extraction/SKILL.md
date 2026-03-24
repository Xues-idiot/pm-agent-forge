# 说话人提取 (Speaker Extraction)

## Overview

说话人提取是识别和分离播客中不同说话人的技能。用于区分主持人和嘉宾、追踪说话时间等。

## 何时使用

- 区分主持人和嘉宾
- 追踪谁说了什么
- 分析对话结构
- 生成对话摘要

## 流程

1. **说话人检测**：检测有多少说话人
2. **声音分离**：分离各说话人音频
3. **声纹识别**：识别说话人身份
4. **时间追踪**：追踪各段发言时间
5. **标注输出**：输出说话人标注
6. **验证校验**：人工校验
7. **学习优化**：持续优化识别

## 模板

### 说话人识别配置模板
```python
SPEAKER_CONFIG = {
    "diarization": {
        "min_speakers": 1,
        "max_speakers": 10
    },
    "identification": {
        "known_speakers": ["主持人A", "嘉宾B"],
        "threshold": 0.8
    }
}

def extract_speakers(transcription: Transcription) -> List[SpeakerSegment]:
    """提取说话人"""
    # 说话人分离
    segments = pyannote.diarize(transcription.audio)

    # 声纹识别
    for segment in segments:
        speaker_id = identify_speaker(segment.embedding)
        segment.speaker = speaker_id

    return segments
```

## 检查清单

- [ ] 说话人数量准确
- [ ] 身份识别正确
- [ ] 时间戳精确
- [ ] 标注清晰
- [ ] 可纠错
- [ ] 持续学习

## 红牌警告

- 说话人数量错误
- 身份混淆
- 时间戳不准
- 无法识别新说话人
- 背景噪音干扰
