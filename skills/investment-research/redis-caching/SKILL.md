# Redis缓存策略 (Redis Caching)

## Overview

Redis缓存策略是使用Redis优化投研系统性能的技能。缓存行情数据、研报结果，减少重复计算。

## 何时使用

- 热点数据缓存
- 会话管理
- 实时行情
- 计算结果缓存

## 流程

1. **缓存设计**：设计缓存策略
2. **Key设计**：设计缓存Key
3. **TTL设计**：设计过期策略
4. **实现**：实现缓存逻辑
5. **监控**：监控缓存效果
6. **优化**：优化缓存命中率
7. **降级**：设计降级策略

## 模板

### Redis缓存模板
```python
import redis
import json
from functools import wraps

redis_client = redis.Redis(host='localhost', port=6379, db=0)

def cache_result(expire: int = 300):
    """缓存装饰器"""
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            # 生成cache key
            cache_key = f"{func.__name__}:{str(args)}:{str(kwargs)}"

            # 尝试获取缓存
            cached = redis_client.get(cache_key)
            if cached:
                return json.loads(cached)

            # 执行函数
            result = func(*args, **kwargs)

            # 设置缓存
            redis_client.setex(cache_key, expire, json.dumps(result))
            return result
        return wrapper
    return decorator

@cache_result(expire=60)  # 60秒缓存
def get_realtime_price(stock_code: str) -> dict:
    """获取实时股价"""
    return fetch_price_from_api(stock_code)

@cache_result(expire=3600)  # 1小时缓存
def get_financial_data(stock_code: str) -> dict:
    """获取财务数据"""
    return fetch_financial_from_db(stock_code)
```

## 检查清单

- [ ] Key设计规范
- [ ] TTL合理
- [ ] 缓存命中率
- [ ] 内存使用
- [ ] 降级策略
- [ ] 监控告警

## 红牌警告

- Key冲突
- TTL过长数据过期
- 缓存穿透
- 缓存雪崩
- 内存溢出
