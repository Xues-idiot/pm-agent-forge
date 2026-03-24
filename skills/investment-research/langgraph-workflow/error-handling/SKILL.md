# 错误处理 (Error Handling)

## Overview

错误处理是在Agent执行过程中捕获、处理和恢复异常的技能。确保系统稳定性和容错能力。

## 何时使用

- API调用可能失败
- 数据采集可能超时
- Agent执行可能异常
- 需要优雅降级

## 流程

1. **错误识别**：识别可能出错环节
2. **错误分类**：区分可恢复/不可恢复错误
3. **重试策略**：设计重试机制
4. **降级策略**：设计降级方案
5. **错误传播**：处理错误传播
6. **日志记录**：记录错误详情
7. **恢复机制**：设计恢复流程

## 模板

### 错误处理模板
```python
from typing import Optional
from tenacity import retry, stop_after_attempt, wait_exponential
import logging

logger = logging.getLogger(__name__)

class AgentError(Exception):
    """Agent执行异常"""
    def __init__(self, agent_name: str, error: str, recoverable: bool = True):
        self.agent_name = agent_name
        self.error = error
        self.recoverable = recoverable
        super().__init__(f"{agent_name}: {error}")

@retry(stop=stop_after_attempt(3), wait=wait_exponential(multiplier=1, min=2, max=10))
def robust_api_call(api_func, *args, **kwargs):
    """带重试的API调用"""
    try:
        return api_func(*args, **kwargs)
    except Exception as e:
        logger.warning(f"API call failed: {e}, retrying...")
        raise

def error_handler(state: ResearchState, error: Exception) -> ResearchState:
    """统一错误处理"""
    if isinstance(error, AgentError):
        state["error"] = str(error)
        state["agent_results"].append({
            "agent_name": error.agent_name,
            "status": "failed",
            "error": str(error),
            "recoverable": error.recoverable
        })

        if error.recoverable:
            # 可恢复错误，标记重试
            logger.info(f" recoverable error in {error.agent_name}")
        else:
            # 不可恢复错误，更新状态
            state["status"] = "failed"
    else:
        state["error"] = f"Unexpected error: {error}"
        state["status"] = "failed"

    return state

# 使用try-except包装Agent
def wrapped_agent(agent_func):
    def wrapper(state: ResearchState) -> ResearchState:
        try:
            return agent_func(state)
        except Exception as e:
            return error_handler(state, e)
    return wrapper

# 降级策略示例
def degraded_analysis(state: ResearchState) -> dict:
    """降级分析 - 当完整数据不可用时"""
    if state.get("raw_data") is None:
        # 使用缓存或简化分析
        return {"analysis": "simplified", "source": "cache"}
    else:
        return normal_analysis(state)
```

## 检查清单

- [ ] 错误分类清晰
- [ ] 重试次数合理
- [ ] 降级策略有效
- [ ] 错误日志完整
- [ ] 恢复流程可行
- [ ] 用户提示友好

## 红牌警告

- 错误吞噬导致难调试
- 重试次数过多
- 降级后数据不正确
- 错误日志缺失
- 用户看到原始错误
