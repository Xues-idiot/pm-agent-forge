# 浏览器自动化基础 (Browser Automation)

## Overview

浏览器自动化基础是使用Playwright/Selenium等工具控制浏览器的技能。是垂直浏览器Agent的核心能力。

## 何时使用

- 网页内容抓取
- 表单自动填写
- 自动化测试
- 定时任务执行

## 流程

1. **环境搭建**：安装浏览器驱动
2. **页面导航**：打开和导航页面
3. **元素定位**：定位页面元素
4. **交互执行**：点击、输入、滚动
5. **内容提取**：提取页面内容
6. **异常处理**：处理反爬和异常
7. **结果保存**：保存抓取结果

## 模板

### Playwright模板
```python
from playwright.async_api import async_playwright

async def scrape_page(url: str) -> dict:
    async with async_playwright() as p:
        browser = await p.chromium.launch(headless=True)
        page = await browser.new_page()

        await page.goto(url)
        await page.wait_for_load_state("networkidle")

        # 提取内容
        content = await page.content()
        title = await page.title()

        await browser.close()
        return {"title": title, "content": content}
```

## 检查清单

- [ ] 元素定位准确
- [ ] 等待策略合理
- [ ] 反反爬处理
- [ ] 错误处理完善
- [ ] 结果提取准确
- [ ] 资源清理

## 红牌警告

- 元素定位脆弱
- 页面未加载完成
- 被反爬拦截
- 资源泄漏
- 结果不完整
