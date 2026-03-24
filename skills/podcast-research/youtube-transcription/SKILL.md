# YouTube视频处理 (YouTube Processing)

## Overview

YouTube视频处理是处理YouTube视频/直播的技能。包括字幕提取、章节识别、评论分析等。

## 何时使用

- 处理YouTube视频内容
- 分析YouTube评论
- 频道研究
- YouTube内容采集

## 流程

1. **链接解析**：解析YouTube链接
2. **字幕获取**：获取字幕/CC
3. **章节提取**：提取视频章节
4. **评论获取**：获取视频评论
5. **评论分析**：分析评论内容
6. **频道信息**：提取频道信息
7. **数据整理**：整理分析数据

## 模板

### YouTube处理配置
```python
YOUTUBE_CONFIG = {
    "quality": "best",
    "subtitle_langs": ["zh", "en", "ja"],
    "comments_limit": 100,
    "include_replies": False
}

async def process_youtube(url: str) -> VideoContent:
    """处理YouTube视频"""
    # 获取视频信息
    video_info = await youtube_api.get_video_info(url)

    # 获取字幕
    transcript = await youtube_api.get_transcript(url)

    # 获取章节
    chapters = await youtube_api.get_chapters(url)

    # 获取评论
    comments = await youtube_api.get_comments(url, limit=100)

    return VideoContent(
        title=video_info.title,
        description=video_info.description,
        transcript=transcript,
        chapters=chapters,
        comments=comments,
        channel=Channel(
            name=video_info.channel_title,
            subscribers=video_info.subscriber_count,
            total_views=video_info.view_count
        )
    )
```

## 检查清单

- [ ] 字幕获取准确
- [ ] 章节识别正确
- [ ] 评论获取完整
- [ ] 频道信息准确
- [ ] API配额管理
- [ ] 内容版权

## 红牌警告

- 字幕不可用
- API配额限制
- 评论关闭
- 地域限制
- 版权问题
