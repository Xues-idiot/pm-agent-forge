# 社交媒体垂直浏览器 (Social Media Browser)

## Overview

社交媒体垂直浏览器是自动化操作社交媒体平台的技能。包括内容发布、互动、数据采集等。

## 何时使用

- 社交媒体管理
- 批量内容发布
- 数据分析
- 竞品监控

## 流程

1. **平台选择**：选择目标平台
2. **认证管理**：管理登录认证
3. **操作设计**：设计自动化操作
4. **内容准备**：准备发布内容
5. **执行操作**：执行自动化操作
6. **结果验证**：验证操作结果
7. **数据记录**：记录操作数据

## 模板

### 社交媒体操作模板
```python
class SocialMediaBrowser:
    def __init__(self, platform: str):
        self.platform = platform
        self.browser = None

    async def login(self, credentials: dict):
        """登录"""
        await self.browser.goto(f"{self.platform}/login")
        await self.browser.fill("[name=username]", credentials["username"])
        await self.browser.fill("[name=password]", credentials["password"])
        await self.browser.click("[type=submit]")

    async def post_content(self, content: str, images: list = None):
        """发布内容"""
        await self.browser.goto(f"{self.platform}/compose")
        await self.browser.fill("[contenteditable]", content)
        if images:
            await self.browser.set_input_files("[type=file]", images)
        await self.browser.click("[submit]")

    async def scrape_posts(self, hashtag: str, limit: int = 100):
        """采集帖子"""
        await self.browser.goto(f"{self.platform}/explore/{hashtag}")
        posts = []
        while len(posts) < limit:
            await self.browser.scroll_down()
            new_posts = await self.browser.extract_posts()
            posts.extend(new_posts)
        return posts[:limit]
```

## 检查清单

- [ ] 登录稳定
- [ ] 操作模拟真实
- [ ] 反爬绕过
- [ ] 结果验证
- [ ] 数据准确
- [ ] 合规使用

## 红牌警告

- 账号被封
- 操作过于频繁
- 违反平台规则
- 数据不准确
- 隐私问题
