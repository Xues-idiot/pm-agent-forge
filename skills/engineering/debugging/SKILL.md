---
name: engineering-debugging
description: Use when debugging code issues, diagnosing AI feature problems, or tracing production bugs. Covers systematic debugging approaches, AI feature debugging (4D audit), and common patterns.
---

# Engineering Debugging

系统化调试代码问题，诊断AI功能异常。

## 何时使用

- 代码出现Bug需要定位
- AI功能输出异常
- 生产环境问题排查
- 调试方法论学习

## 标准调试流程

### 1. 问题定义

**调试问题模板：**
```markdown
## 问题描述

### 现象
[具体描述可观察的错误]

### 环境
- 系统: Windows/Mac/Linux
- 语言版本: Python 3.9+
- 复现步骤: 1, 2, 3...

### 预期行为
[应该怎样]

### 实际行为
[实际怎样]
```

### 2. 复现问题

**最小复现示例：**
```python
# 创建一个最小可复现的代码片段
import pytest

def test_bug_reproduction():
    """最小复现：输入X期望Y实际Z"""
    result = your_function("input")
    assert result == "expected_output"
```

**复现检查清单：**
- [ ] 问题是否稳定复现？
- [ ] 是否只在特定条件下出现？
- [ ] 是否与数据相关？
- [ ] 是否与并发相关？

### 3. 二分定位法

```
日志范围: [开始] ────────────────── [结束]
              ↓
         取中点加日志
              ↓
         [开始] ───── [中点]    [中点] ───── [结束]
              ↓                   ↓
          哪半有问题？            哪半有问题？
              ↓                   ↓
         继续二分              继续二分
```

### 4. 常见问题模式

| 问题类型 | 典型症状 | 排查方向 |
|----------|----------|----------|
| 空指针 | `None is not callable` | 初始化、边界条件 |
| 数组越界 | `IndexError` | 长度检查、边界计算 |
| 并发问题 | 间歇性错误 | 锁、线程安全 |
| 内存泄漏 | 内存持续增长 | 对象引用、缓存 |
| API超时 | Request Timeout | 网络、限流、慢查询 |

### 5. 日志调试

**日志级别使用：**
```python
import logging

logger = logging.getLogger(__name__)

# DEBUG: 开发时详细信息
logger.debug(f"Processing item: {item_id}")

# INFO: 关键业务流程
logger.info(f"Order {order_id} created successfully")

# WARNING: 需要关注但不阻断
logger.warning(f"Retry attempt {attempt} for {item_id}")

# ERROR: 错误需要调查
logger.error(f"Failed to process {item_id}: {e}", exc_info=True)
```

**结构化日志：**
```json
{
  "timestamp": "2026-03-23T10:00:00Z",
  "level": "ERROR",
  "service": "order-service",
  "trace_id": "abc123",
  "user_id": "user_456",
  "message": "Order creation failed",
  "error": {
    "type": "PaymentDeclined",
    "code": "PAYMENT_001"
  }
}
```

## AI功能调试 (4D审计)

> 来自Pi项目的ai-debug skill方法论

### D1: Job定义清晰吗？

**检查项：**
- 能准确描述模型应该输出什么？
- 输入输出有书面规范？
- 工程师和PM对"好"有一致定义？

**诊断模板：**
```markdown
## D1: Job定义检查

| 检查项 | 状态 | 说明 |
|--------|------|------|
| 输出格式定义 | ✅/❌ | |
| 输入类型定义 | ✅/❌ | |
| 边界条件定义 | ✅/❌ | |
| 质量标准定义 | ✅/❌ | |
```

### D2: 上下文正确吗？

**上下文6层模型：**
1. **Intent** - 用户意图
2. **User** - 用户特征
3. **Domain** - 领域知识
4. **Rules** - 业务规则
5. **Environment** - 环境状态
6. **Exposition** - 展示上下文

**检查方法：**
```python
# 检查实际发送给模型的上下文
def audit_context(model_input):
    context_layers = {
        "intent": extract_intent(model_input),
        "user": extract_user_context(model_input),
        "domain": extract_domain_knowledge(model_input),
        "rules": extract_business_rules(model_input),
        "environment": extract_env_state(model_input),
        "exposition": extract_display_context(model_input),
    }

    for layer, content in context_layers.items():
        print(f"{layer}: {len(content)} chars, {content[:100]}...")
```

### D3: 上下文获取可靠吗？

- 运行时如何获取各类上下文？
- 数据源不可用时怎么办？
- 每个请求用了哪些上下文有可见性？

### D4: 失败被捕获了吗？

- 调用模型前有预检查？
- 输出后有验证？
- 失败时的UX是什么？
- 有反馈循环捕获失败？

## 调试检查清单

**通用调试：**
- [ ] 问题可复现
- [ ] 最小复现案例创建
- [ ] 日志充足
- [ ] 假设被验证/否定
- [ ] 根因确定

**AI调试：**
- [ ] D1: Job定义清晰
- [ ] D2: 上下文正确完整
- [ ] D3: 上下文获取可靠
- [ ] D4: 失败被捕获

## 红牌警告

- 不写日志就调试
- 猜测根因不验证
- 修复不测试就上线
- 同样的问题反复出现
- 不记录复现步骤

## 好/坏对比

**好调试：**
```
1. 现象：API响应时间从100ms增加到2000ms
2. 假设：数据库查询变慢
3. 验证：添加SQL日志，发现某查询从5ms增加到1900ms
4. 根因：缺少索引
5. 修复：添加索引，响应恢复到100ms
6. 验证：复现案例通过
```

**坏调试：**
```
"可能是缓存问题，清一下缓存试试"
（不验证，不记录，不学习）
```
