# 招聘垂直浏览器 (Recruitment Browser)

## Overview

招聘垂直浏览器是自动化操作招聘平台的技能。包括职位搜索、简历投递、机会追踪等。

## 何时使用

- 批量职位搜索
- 简历投递自动化
- 机会对比分析
- 面试追踪

## 流程

1. **平台管理**：管理招聘平台账号
2. **条件设置**：设置求职条件
3. **职位搜索**：搜索匹配职位
4. **筛选过滤**：筛选过滤职位
5. **投递申请**：自动化投递
6. **状态追踪**：追踪申请状态
7. **数据分析**：分析求职效果

## 模板

### 招聘自动化模板
```python
async def job_hunt(config: JobHuntConfig):
    """自动化求职"""
    jobs = []

    # 搜索职位
    for platform in config.platforms:
        await page.goto(f"{platform}/jobs")
        await page.fill(".search-input", config.keywords)
        await page.apply_filters(config.filters)
        await page.click(".search-btn")

        results = await page.extract_job_listings()
        jobs.extend(results)

    # 过滤
    filtered = filter_jobs(jobs, config.criteria)

    # 投递
    for job in filtered[:config.max_applications]:
        await page.goto(job.url)
        await page.fill_resume(config.resume)
        await page.submit_application()

    return {"applied": len(filtered), "jobs": filtered}
```

## 检查清单

- [ ] 登录稳定
- [ ] 搜索准确
- [ ] 过滤合理
- [ ] 投递成功
- [ ] 状态追踪
- [ ] 隐私保护

## 红牌警告

- 账号被封
- 信息不准确
- 投递失败
- 隐私泄露
- 频率过高
