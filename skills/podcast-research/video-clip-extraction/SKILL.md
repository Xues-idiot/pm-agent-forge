# 视频剪辑提取 (Video Clip Extraction)

## Overview

视频剪辑提取是将长视频/播客剪辑成短片段的技能。

## 何时使用

- 制作精彩片段
- 社交媒体分享
- 短视频制作
- 内容推广

## 流程

1. **精彩时刻识别**：识别精彩片段
2. **剪辑点确定**：确定剪辑起止点
3. **视频剪辑**：执行视频剪辑
4. **字幕处理**：处理字幕
5. **格式转换**：转换输出格式
6. **质量优化**：优化输出质量
7. **元数据**：添加元数据

## 模板

### 剪辑提取配置
```python
CLIP_CONFIG = {
    "min_duration": 30,  # 最小30秒
    "max_duration": 180,  # 最大3分钟
    "overlap": 5,  # 片段间重叠5秒
    "output_format": "mp4",
    "quality": "1080p"
}

async def extract_clips(video_path: str, key_moments: List[KeyMoment]) -> List[Clip]:
    """提取精彩片段"""
    clips = []

    for moment in key_moments:
        start = max(0, moment.start - 5)  # 提前5秒
        end = min(video_duration, moment.end + 5)  # 延后5秒

        # 剪辑
        clip_path = await video_editor.trim(
            video_path,
            start=start,
            end=end
        )

        # 添加字幕
        clip_with_subtitle = await add_subtitles(
            clip_path,
            subtitles=moment.related_subtitles
        )

        clips.append(Clip(
            path=clip_with_subtitle,
            start=start,
            end=end,
            description=moment.description,
            hashtags=extract_hashtags(moment)
        ))

    return clips
```

## 检查清单

- [ ] 时刻识别准确
- [ ] 剪辑点合适
- [ ] 字幕同步
- [ ] 格式正确
- [ ] 质量达标
- [ ] 元数据完整

## 红牌警告

- 时刻误判
- 剪辑点不当
- 字幕不同步
- 画质损失
- 格式不兼容
