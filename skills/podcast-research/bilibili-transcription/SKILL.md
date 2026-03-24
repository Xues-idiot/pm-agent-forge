# B站视频处理 (Bilibili Processing)

## Overview

B站视频处理是专门处理B站视频/直播的技能。包括字幕提取、弹幕分析、UP主信息等。

## 何时使用

- 处理B站视频内容
- 分析B站弹幕
- UP主研究
- B站内容采集

## 流程

1. **链接解析**：解析B站视频链接
2. **字幕获取**：获取字幕/弹幕
3. **内容提取**：提取视频内容
4. **弹幕分析**：分析弹幕内容
5. **UP主信息**：提取UP主信息
6. **数据整理**：整理分析数据
7. **跨平台整合**：与其他平台整合

## 模板

### B站处理配置
```python
BILIBILI_CONFIG = {
    "quality": "1080P",
    "subtitle_langs": ["zh-CN", "zh-TW", "en"],
    "danmaku": True,
    "cookie": "your_cookies"
}

async def process_bilibili(url: str) -> VideoContent:
    """处理B站视频"""
    # 获取视频信息
    video_info = await bilibili_api.get_video_info(url)

    # 下载字幕
    subtitles = await bilibili_api.get_subtitles(url)

    # 获取弹幕
    danmaku = await bilibili_api.get_danmaku(video_info.cid)

    # 提取字幕文本
    text = "".join([s.text for s in subtitles])

    return VideoContent(
        title=video_info.title,
        description=video_info.description,
        subtitles=subtitles,
        danmaku=danmaku,
        text=text,
        uploader=video_info.uploader,
        uploader_fans=video_info.fans
    )
```

## 检查清单

- [ ] 链接解析正确
- [ ] 字幕获取完整
- [ ] 弹幕分析准确
- [ ] UP主信息准确
- [ ] 画质选择合适
- [ ] 存储管理

## 红牌警告

- 字幕获取失败
- B站反爬
- Cookie失效
- 画质不佳
- 内容违规
