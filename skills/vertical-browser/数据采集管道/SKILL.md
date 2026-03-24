# 数据采集管道 (Data Pipeline)

## Overview

数据采集管道是构建完整网页数据采集流程的技能。包括调度、采集、清洗、存储全链路。

## 何时使用

- 大规模数据采集
- 持续数据更新
- 多源数据聚合
- 数据质量控制

## 流程

1. **任务设计**：设计采集任务
2. **调度配置**：配置采集调度
3. **采集执行**：执行采集
4. **数据清洗**：清洗数据
5. **质量控制**：控制数据质量
6. **存储管理**：存储数据
7. **监控告警**：监控管道运行

## 模板

### 数据管道模板
```python
class DataPipeline:
    def __init__(self):
        self.sources = []
        self.extractors = {}
        self.storage = Storage()

    def add_source(self, name: str, url: str, extractor: callable):
        """添加数据源"""
        self.sources.append({"name": name, "url": url, "extractor": extractor})

    async def run(self):
        """运行管道"""
        results = []

        for source in self.sources:
            try:
                # 采集
                raw_data = await self.collect(source)

                # 清洗
                cleaned = await self.clean(raw_data)

                # 质量检查
                if self.quality_check(cleaned):
                    # 存储
                    await self.storage.save(source["name"], cleaned)
                    results.append({"source": source["name"], "status": "success"})
                else:
                    results.append({"source": source["name"], "status": "quality_failed"})

            except Exception as e:
                results.append({"source": source["name"], "status": "error", "error": str(e)})

        return results

    async def schedule(self, cron_expr: str):
        """定时调度"""
        schedule(cron_expr, self.run)
```

## 检查清单

- [ ] 任务设计合理
- [ ] 调度稳定
- [ ] 采集准确
- [ ] 清洗有效
- [ ] 质量达标
- [ ] 监控完善

## 红牌警告

- 任务失败
- 数据丢失
- 重复采集
- 质量不达标
- 存储溢出
- 监控缺失
