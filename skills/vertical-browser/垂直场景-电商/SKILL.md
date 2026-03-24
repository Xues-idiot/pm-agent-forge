# 电商垂直浏览器 (E-commerce Browser)

## Overview

电商垂直浏览器是自动化操作电商平台的技能。包括商品搜索、价格监控、订单管理等。

## 何时使用

- 价格监控
- 商品比价
- 批量下单
- 竞品分析

## 流程

1. **目标平台**：选择电商平台
2. **认证管理**：管理登录
3. **搜索采集**：搜索和采集商品
4. **价格监控**：监控价格变化
5. **订单操作**：执行订单操作
6. **数据整理**：整理分析数据
7. **告警通知**：价格告警通知

## 模板

### 电商监控模板
```python
async def monitor_price(product_url: str, target_price: float):
    """监控商品价格"""
    browser = await launch_browser()
    page = await browser.new_page()

    await page.goto(product_url)
    await page.wait_for_selector(".price")

    current_price = await page.extract_price(".price")
    product_name = await page.extract_text(".product-title")

    if current_price <= target_price:
        await send_alert(f"{product_name} 价格低于 {target_price}，当前价格 {current_price}")

    await browser.close()
    return {"product": product_name, "price": current_price}

async def scrape_search_results(keyword: str, pages: int = 5):
    """采集搜索结果"""
    results = []
    for page_num in range(pages):
        url = f"https://ecommerce.example.com/search?q={keyword}&page={page_num}"
        await page.goto(url)
        items = await page.extract_items(".product-item")
        results.extend(items)
    return results
```

## 检查清单

- [ ] 登录稳定
- [ ] 数据准确
- [ ] 价格提取正确
- [ ] 反爬绕过
- [ ] 监控持续
- [ ] 告警及时

## 红牌警告

- 账号被封
- 数据延迟
- 价格不准确
- 页面结构变化
- 恶意竞争
