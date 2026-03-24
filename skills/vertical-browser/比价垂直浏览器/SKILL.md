# 比价垂直浏览器 (Price Comparison Browser)

## Overview

比价垂直浏览器是专门用于跨平台价格比较的技能。支持同款商品多平台价格对比、历史价格查询等。

## 何时使用

- 跨平台比价
- 历史价格追踪
- 最低价提醒
- 优惠信息聚合
- 购买决策支持

## 流程

1. **商品识别**：识别同款商品
2. **平台采集**：采集多平台价格
3. **价格对比**：对比价格差异
4. **历史分析**：分析价格历史
5. **优惠计算**：计算最终优惠
6. **推荐生成**：生成购买建议

## 模板

### 比价模板
```python
class PriceComparisonBrowser:
    def __init__(self):
        self.platforms = {
            "jd": JDSpider(),
            "taobao": TaobaoSpider(),
            "pdd": PddSpider(),
            "amazon": AmazonSpider()
        }

    async def compare_price(self, product_name: str):
        """比价"""
        # 1. 各平台搜索
        results = {}
        for platform, spider in self.platforms.items():
            try:
                products = await spider.search(product_name)
                results[platform] = self.normalize_products(products)
            except Exception as e:
                results[platform] = []

        # 2. 商品匹配
        matched = self.match_same_products(results)

        # 3. 价格排序
        sorted_products = sorted(
            matched,
            key=lambda x: x["price"]
        )

        return PriceComparisonResult(
            product=product_name,
            alternatives=sorted_products,
            best_price=sorted_products[0] if sorted_products else None,
            price_diff=self.calculate_price_diff(sorted_products)
        )

    async def track_price_history(self, product_url: str):
        """追踪价格历史"""
        history = []
        for _ in range(30):
            price = await self.get_current_price(product_url)
            history.append({"date": datetime.now(), "price": price})
            await asyncio.sleep(3600)

        return {
            "current": history[-1]["price"],
            "avg": sum(h["price"] for h in history) / len(history),
            "min": min(h["price"] for h in history),
            "max": max(h["price"] for h in history),
            "trend": self.analyze_trend(history)
        }
```

## 检查清单

- [ ] 平台覆盖
- [ ] 数据准确
- [ ] 匹配正确
- [ ] 分析深入

## 红牌警告

- 数据缺失
- 匹配错误
- 价格滞后
- 分析偏差
