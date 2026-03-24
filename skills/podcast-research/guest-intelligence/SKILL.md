# 嘉宾情报分析 (Guest Intelligence)

## Overview

嘉宾情报分析是挖掘和分析播客嘉宾背景信息的技能。包括嘉宾履历、社交关系、历史发言等。

## 何时使用

- 嘉宾背景调查
- 历史内容回顾
- 话题预判
- 关系图谱
- 价值评估

## 流程

1. **嘉宾识别**：识别嘉宾身份
2. **信息采集**：采集嘉宾信息
3. **背景分析**：分析教育、工作背景
4. **社交关系**：构建社交关系图
5. **历史发言**：分析历史发言风格
6. **话题匹配**：匹配擅长话题
7. **报告生成**：生成嘉宾报告

## 模板

### 嘉宾情报模板
```python
class GuestIntelligence:
    def __init__(self):
        self.social_scraper = SocialMediaScraper()
        self.news_analyzer = NewsAnalyzer()
        self.kg_builder = KnowledgeGraphBuilder()

    async def analyze_guest(self, guest_name: str, platform: str = None):
        """分析嘉宾"""
        # 1. 获取基本信息
        basic_info = await self.get_basic_info(guest_name)

        # 2. 采集社交媒体
        social_data = await self.social_scraper.scrape(guest_name)

        # 3. 分析新闻报道
        news_data = await self.news_analyzer.search(guest_name)

        # 4. 构建关系图谱
        relations = await self.kg_builder.build_person_graph(guest_name)

        # 5. 分析发言风格
        speaking_style = await self.analyze_speaking_style(guest_name)

        # 6. 话题专长分析
        expertise = await self.analyze_expertise(guest_name)

        return GuestProfile(
            name=guest_name,
            basic_info=basic_info,
            social_data=social_data,
            news_data=news_data,
            relations=relations,
            speaking_style=speaking_style,
            expertise=expertise
        )

    async def generate_intro(self, guest: GuestProfile) -> str:
        """生成嘉宾介绍"""
        template = f"{guest.name}，"
        if guest.basic_info.get('title'):
            template += f"{guest.basic_info['title']}，"
        if guest.basic_info.get('company'):
            template += f"{guest.basic_info['company']}，"
        if guest.expertise:
            template += f"在{'、'.join(guest.expertise[:3])}领域有深厚积累。"
        return template
```

## 检查清单

- [ ] 信息准确
- [ ] 关系完整
- [ ] 分析深入
- [ ] 报告专业

## 红牌警告

- 信息错误
- 隐私泄露
- 关系错误
- 分析偏差
