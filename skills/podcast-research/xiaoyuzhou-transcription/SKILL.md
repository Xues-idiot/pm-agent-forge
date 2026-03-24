# 小宇宙播客处理 (Xiaoyuzhou Processing)

## Overview

小宇宙是中文播客平台，专注于播客内容的处理技能。

## 何时使用

- 处理小宇宙播客
- 中文播客研究
- 中文播客发现
- 播客订阅管理

## 流程

1. **播客发现**：发现小宇宙播客
2. **Episode获取**：获取播客列表
3. **音频下载**：下载音频
4. **转写处理**：转写为文字
5. **内容分析**：分析内容
6. **订阅管理**：管理订阅
7. **数据整合**：跨平台整合

## 模板

### 小宇宙处理配置
```python
XIAOYUZHOU_CONFIG = {
    "download_path": "./podcasts/xiaoyuzhou",
    "transcribe": True,
    "transcribe_lang": "zh"
}

async def process_xiaoyuzhou(podcast_id: str):
    """处理小宇宙播客"""
    # 获取播客信息
    podcast = await xiaoyuzhou_api.get_podcast(podcast_id)

    # 获取最新 episodes
    episodes = await xiaoyuzhou_api.get_episodes(podcast_id)

    # 下载并转写最新 episode
    latest = episodes[0]
    audio_path = await download_audio(latest.audio_url)
    transcript = await transcribe(audio_path)

    return {
        "podcast": podcast,
        "episode": latest,
        "transcript": transcript
    }
```

## 检查清单

- [ ] API可用
- [ ] 音频下载完整
- [ ] 转写准确
- [ ] 内容分析
- [ ] 订阅管理
- [ ] 跨平台整合

## 红牌警告

- API变更
- 音频下载失败
- 转写质量差
- 内容不完整
- 同步失败
