# FastAPI后端服务 (FastAPI Backend)

## Overview

FastAPI后端服务是构建投研Agent后端API的技能。参考FinSight的API设计，提供RESTful接口供前端调用。

## 何时使用

- 构建投研API服务
- 支持前端调用
- 多用户支持
- 微服务架构

## 流程

1. **API设计**：设计接口
2. **数据层**：实现数据访问
3. **业务层**：实现业务逻辑
4. **Agent集成**：集成Agent能力
5. **认证授权**：实现认证
6. **测试验证**：测试API
7. **部署上线**：部署服务

## 模板

### FastAPI模板
```python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel
from typing import Optional
import uvicorn

app = FastAPI(title="投研Agent API", version="1.0.0")

class ResearchRequest(BaseModel):
    stock_code: str
    task_type: str = "stock"  # stock/industry/macro
    depth: str = "full"  # quick/full

class ResearchResponse(BaseModel):
    task_id: str
    status: str
    report: Optional[str] = None
    investment_advice: Optional[str] = None

@app.post("/api/v1/research", response_model=ResearchResponse)
async def research_stock(request: ResearchRequest):
    """研究股票"""
    task_id = generate_task_id()
    # 调用Agent执行研究
    result = await agent.research(request)
    return ResearchResponse(task_id=task_id, **result)

@app.get("/api/v1/research/{task_id}")
async def get_research_status(task_id: str):
    """获取研究状态"""
    return get_task_status(task_id)

@app.get("/api/v1/stock/{stock_code}/price")
async def get_stock_price(stock_code: str):
    """获取实时股价"""
    return get_realtime_price(stock_code)

if __name__ == "__main__":
    uvicorn.run(app, host="0.0.0.0", port=8000)
```

## 检查清单

- [ ] API设计RESTful
- [ ] 错误处理完善
- [ ] 认证授权安全
- [ ] 性能优化
- [ ] 文档完善
- [ ] 测试覆盖

## 红牌警告

- API不安全
- 错误处理不当
- 性能问题
- 文档缺失
- 测试不足
