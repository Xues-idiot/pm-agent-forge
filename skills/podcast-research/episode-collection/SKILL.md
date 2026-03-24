# Episode采集 (Episode Collection)

## Overview

Episode采集是自动抓取、下载、管理播客 episodes 的技能。支持批量下载、断点续传、自动归档。

## 何时使用

- 批量下载 episodes
- 自动下载新 episodes
- 离线播放准备
- 构建本地播客库

## 流程

1. **订阅源管理**：管理播客RSS源
2. **Episode扫描**：扫描新 episodes
3. **下载队列**：加入下载队列
4. **下载执行**：执行下载任务
5. **元数据获取**：获取节目信息
6. **存储管理**：管理本地存储
7. **清理归档**：过期内容清理归档

## 模板

### Episode下载配置模板
```python
DOWNLOAD_CONFIG = {
    "parallel_downloads": 3,
    "max_retries": 3,
    "timeout": 300,
    "storage_path": "./podcasts/{podcast_name}/{episode_title}.mp3",
    "auto_cleanup": {
        "enabled": True,
        "keep_days": 30,
        "keep_unplayed": True
    }
}

async def download_episode(episode: Episode, config: DownloadConfig):
    """下载单个episode"""
    url = episode.audio_url
    path = config.storage_path.format(
        podcast_name=sanitize_filename(episode.podcast),
        episode_title=sanitize_filename(episode.title)
    )
    await async_download(url, path, retry=config.max_retries)
    return path
```

## 检查清单

- [ ] 下载稳定
- [ ] 断点续传
- [ ] 元数据完整
- [ ] 存储管理
- [ ] 清理机制
- [ ] 磁盘空间

## 红牌警告

- 下载失败
- 存储混乱
- 磁盘空间不足
- 元数据丢失
- 重复下载
