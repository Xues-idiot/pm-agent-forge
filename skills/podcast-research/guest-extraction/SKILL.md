# 嘉宾信息提取 (Guest Extraction)

## Overview

嘉宾信息提取是从播客中识别和整理嘉宾信息的技能。包括职业、背景、观点、主要发言等。

## 何时使用

- 了解嘉宾背景
- 追踪嘉宾动态
- 整理嘉宾库
- 分析嘉宾价值

## 流程

1. **嘉宾识别**：识别嘉宾段落
2. **自我介绍提取**：提取自我介绍
3. **背景查询**：查询嘉宾信息
4. **观点提取**：提取嘉宾观点
5. **关系图谱**：构建关系图谱
6. **信息存储**：存储嘉宾信息
7. **动态更新**：追踪嘉宾动态

## 模板

### 嘉宾信息模板
```python
@dataclass
class Guest:
    name: str
    title: str
    company: str
    bio: str
    expertise: List[str]
    appearances: List[Appearance]
    social_media: Dict[str, str]

def extract_guest_info(episode: Episode) -> List[Guest]:
    """提取嘉宾信息"""
    # 识别嘉宾段落（自我介绍）
    intro_segments = identify_introductions(episode.transcription)

    guests = []
    for segment in intro_segments:
        # 提取姓名和头衔
        info = parse_introduction(segment.text)

        # 查询补充信息
        full_info = await enrich_guest_info(info)

        guests.append(Guest(**full_info))

    return guests
```

## 检查清单

- [ ] 识别准确
- [ ] 信息完整
- [ ] 去重正确
- [ ] 关系准确
- [ ] 更新及时
- [ ] 隐私保护

## 红牌警告

- 嘉宾识别错误
- 信息不准确
- 隐私问题
- 去重失败
- 更新遗漏
