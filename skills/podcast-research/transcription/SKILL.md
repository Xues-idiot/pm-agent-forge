# 语音转写 (Transcription)

## Overview

语音转写是将播客音频转换为文字的技能。用于搜索、笔记、翻译等后续处理。

## 何时使用

- 生成文字稿
- 搜索播客内容
- 翻译播客
- 做笔记标注

## 流程

1. **音频处理**：提取/切片音频
2. **转写服务**：调用转写API
3. **后处理**：标点恢复、大小写
4. **时间戳**：同步时间戳
5. **质量校验**：校验转写质量
6. **格式导出**：导出多种格式
7. **存储管理**：存储转写稿

## 模板

### 转写配置模板
```python
TRANSCRIPTION_CONFIG = {
    "provider": "whisper",  # whisper/faster-whisper/azure
    "model": "base",  # tiny/base/small/medium/large
    "language": "zh",  # auto/zh/en
    "timestamp": True,
    "format": {
        "srt": True,
        "vtt": True,
        "txt": True
    }
}

async def transcribe_episode(episode: Episode) -> Transcription:
    """转写episode"""
    audio = await extract_audio(episode.audio_path)
    result = await whisper.transcribe(audio, **TRANSCRIPTION_CONFIG)

    return Transcription(
        text=result.text,
        segments=result.segments,
        language=result.language,
        confidence=result.avg_logprob
    )
```

## 检查清单

- [ ] 转写准确
- [ ] 时间戳同步
- [ ] 多格式导出
- [ ] 质量校验
- [ ] 成本控制
- [ ] 批量处理

## 红牌警告

- 转写错误多
- 时间戳不同步
- 专业术语错误
- 成本过高
- 格式不兼容
