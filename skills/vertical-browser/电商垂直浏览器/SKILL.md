# 电商垂直浏览器 (E-commerce Browser)

## Overview

电商垂直浏览器是专门用于电商数据采集和竞争分析的技能。支持淘宝、京东、拼多多等平台。

## 何时使用

- 商品价格监控
- 竞品分析
- 销量追踪
- 评价分析
- 库存监控

## 流程

1. **平台选择**：选择电商平台
2. **商品定位**：定位目标商品
3. **数据采集**：采集商品数据
4. **价格分析**：分析价格走势
5. **竞品对比**：对比竞品数据
6. **监控告警**：设置监控告警
7. **报告生成**：生成分析报告

## 模板

### 电商数据采集模板
```python
class EcommerceBrowser:
    def __init__(self):
        self.platforms = {
            "taobao": TaobaoSpider(),
            "jd": JDSpider(),
            "pdd": PddSpider()
        }

    async def search_products(self, keyword: str, platform: str = None):
        """搜索商品"""
        if platform:
            return await self.platforms[platform].search(keyword)
        results = []
        for p, spider in self.platforms.items():
            results.extend(await spider.search(keyword))
        return self.sort_by_relevance(results)

    async def monitor_price(self, product_url: str, target_price: float):
        """监控价格"""
        price_history = []
        for _ in range(24):  # 监控24小时
            price = await self.get_current_price(product_url)
            price_history.append({"time": datetime.now(), "price": price})
            if price <= target_price:
                await self.send_alert("价格到达目标", product_url, price)
            await asyncio.sleep(3600)
        return self.analyze_price_trend(price_history)

    async def analyze_competitor(self, competitor_id: str):
        """分析竞品"""
        products = await self.search_products(competitor_id)
        return {
            "product_count": len(products),
            "avg_price": self.calculate_avg_price(products),
            "top_sellers": self.get_top_sellers(products),
            "market_share": self.estimate_market_share(products)
        }

    async def track_sales(self, product_id: str, platform: str):
        """追踪销量"""
        current = await self.platforms[platform].get_sales(product_id)
        history = await self.get_sales_history(product_id)
        return {
            "current": current,
            "trend": self.calculate_sales_trend(history),
            "forecast": self.predict_sales(history)
        }
```

## 检查清单

- [ ] 商品覆盖
- [ ] 价格准确
- [ ] 销量真实
- [ ] 分析深入
- [ ] 监控及时
- [ ] 报告专业

## 红牌警告

- 数据缺失
- 价格错误
- 销量虚假
- 封号风险
- 分析偏差
