# 反反爬机制 (Anti-Anti-Bot)

## Overview

反反爬机制是绕过网站反爬虫措施的技能。包括代理轮换、行为模拟、验证码处理等。

## 何时使用

- 高频数据采集
- 敏感网站
- 反爬严格网站
- 需要保持匿名

## 流程

1. **网站分析**：分析反爬机制
2. **策略制定**：制定绕过策略
3. **代理管理**：管理代理池
4. **行为模拟**：模拟人类行为
5. **验证码处理**：处理验证码
6. **请求调度**：控制请求频率
7. **监控调整**：监控效果调整

## 模板

### 反反爬模板
```python
class AntiBotManager:
    def __init__(self):
        self.proxy_pool = ProxyPool()
        self.user_agents = UserAgentPool()
        self.captcha_solver = CaptchaSolver()

    async def get_browser_context(self):
        """获取带反反爬的浏览器上下文"""
        context = await browser.new_context(
            proxy=self.proxy_pool.get(),
            user_agent=self.user_agents.get(),
            extra_http_headers={
                "Accept-Language": "zh-CN,zh;q=0.9",
                "Accept": "text/html,application/xhtml+xml..."
            }
        )

        # 模拟人类行为
        await context.add_init_script("""
            Object.defineProperty(navigator, 'webdriver', {get: () => undefined});
        """)

        return context

    async def solve_captcha(self, image_bytes):
        """解决验证码"""
        return await self.captcha_solver.solve(image_bytes)
```

## 检查清单

- [ ] 代理稳定
- [ ] 行为真实
- [ ] 验证码处理
- [ ] 频率控制
- [ ] 成功率
- [ ] 成本控制

## 红牌警告

- IP被封
- 行为暴露
- 验证码失败
- 请求失败
- 成本过高
- 法律风险
