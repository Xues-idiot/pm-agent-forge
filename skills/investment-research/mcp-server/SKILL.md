# MCP服务器集成 (MCP Server Integration)

## Overview

MCP (Model Context Protocol) 服务器集成是实现Agent标准化数据接口的技能。参考investment-thesis-agent的MCP设计，支持工具调用标准化。

## 何时使用

- 标准化工具调用
- 多数据源接入
- Agent间通信
- 工具共享

## 流程

1. **MCP理解**：理解MCP协议
2. **服务器设计**：设计MCP服务器
3. **工具定义**：定义工具Schema
4. **实现**：实现工具
5. **注册**：注册到Agent
6. **测试**：测试工具调用
7. **文档**：编写文档

## 模板

### MCP服务器模板
```python
from mcp.server import Server
from mcp.types import Tool, Resource
import asyncio

server = Server("investment-research")

@server.list_tools()
async def list_tools() -> list[Tool]:
    return [
        Tool(
            name="get_stock_price",
            description="获取股票实时价格",
            inputSchema={
                "type": "object",
                "properties": {
                    "stock_code": {"type": "string", "description": "股票代码"}
                },
                "required": ["stock_code"]
            }
        ),
        Tool(
            name="get_financial_data",
            description="获取财务报表数据",
            inputSchema={
                "type": "object",
                "properties": {
                    "stock_code": {"type": "string"},
                    "period": {"type": "string", "enum": ["Q1", "Q2", "Q3", "Q4", "annual"]}
                }
            }
        )
    ]

@server.call_tool()
async def call_tool(name: str, arguments: dict) -> str:
    if name == "get_stock_price":
        return await get_stock_price(arguments["stock_code"])
    elif name == "get_financial_data":
        return await get_financial_data(arguments["stock_code"], arguments.get("period"))
    raise ValueError(f"Unknown tool: {name}")

async def main():
    async with server.run() as server:
        await server.stdin_open()

asyncio.run(main())
```

## 检查清单

- [ ] 协议理解正确
- [ ] 工具定义规范
- [ ] 实现正确
- [ ] 测试通过
- [ ] 文档完善
- [ ] 版本管理

## 红牌警告

- Schema不规范
- 实现有bug
- 性能问题
- 安全漏洞
- 版本不兼容
