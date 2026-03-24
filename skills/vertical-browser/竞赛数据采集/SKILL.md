# 竞赛数据采集 (Competition Data Collection)

## Overview

竞赛数据采集是专门用于各类竞赛数据采集和分析的技能。支持ACM、Kaggle、LeetCode等竞赛平台。

## 何时使用

- 竞赛题目采集
- 排名数据分析
- 竞赛趋势分析
- 选手数据追踪
- 竞赛资讯监控

## 流程

1. **平台选择**：选择竞赛平台
2. **数据采集**：采集竞赛数据
3. **排名分析**：分析排名数据
4. **题目分析**：分析竞赛题目
5. **趋势追踪**：追踪竞赛趋势
6. **报告生成**：生成分析报告

## 模板

### 竞赛数据采集模板
```python
class CompetitionCollector:
    def __init__(self):
        self.platforms = {
            "leetcode": LeetCodeSpider(),
            "kaggle": KaggleSpider(),
            "atcoder": AtCoderSpider(),
            "codeforces": CodeForcesSpider()
        }

    async def collect_contest(self, contest_id: str, platform: str):
        """采集竞赛数据"""
        spider = self.platforms[platform]
        contest_info = await spider.get_contest_info(contest_id)
        submissions = await spider.get_submissions(contest_id)
        rankings = await spider.get_rankings(contest_id)

        return ContestData(
            info=contest_info,
            submissions=submissions,
            rankings=rankings,
            platform=platform
        )

    async def analyze_player(self, handle: str, platform: str):
        """分析选手数据"""
        spider = self.platforms[platform]
        profile = await spider.get_profile(handle)
        history = await spider.get_contest_history(handle)

        return {
            "profile": profile,
            "total_contests": len(history),
            "avg_rank": sum(h.rank for h in history) / len(history),
            "rating_trend": self.calculate_rating_trend(history),
            "strengths": self.analyze_strengths(history),
            "weaknesses": self.analyze_weaknesses(history)
        }

    async def track_problem_difficulty(self, platform: str):
        """追踪题目难度"""
        problems = await self.platforms[platform].get_recent_problems()
        return {
            "avg_difficulty": sum(p.difficulty for p in problems) / len(problems),
            "difficulty_distribution": self.distribution(problems),
            "topics": self.analyze_topic_distribution(problems)
        }
```

## 检查清单

- [ ] 数据完整
- [ ] 分析准确
- [ ] 追踪及时
- [ ] 报告专业

## 红牌警告

- 数据缺失
- 分析错误
- 追踪延迟
- 反爬封禁
