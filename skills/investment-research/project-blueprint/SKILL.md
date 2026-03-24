# 项目蓝图与路线图 (Project Blueprint)

## Overview

项目蓝图是规划投研Agent完整项目结构的技能。参考FinSight的项目结构，设计最佳实践。

## 何时使用

- 项目初始化
- 架构设计
- 团队协作
- 进度管理

## 流程

1. **需求分析**：确定需求
2. **架构设计**：设计系统架构
3. **模块划分**：划分项目模块
4. **技术选型**：选择技术栈
5. **时间规划**：制定开发计划
6. **风险管理**：识别风险
7. **质量保障**：制定质量标准

## 模板

### 项目蓝图模板
```
# 投研Agent项目蓝图

## 项目概述
- 项目名称: Investment Research Agent
- 项目目标: 构建多Agent投研系统
- 目标用户: 个人投资者、机构

## 技术架构
### 核心模块
├── agents/              # Agent定义
│   ├── supervisor.py    # 调度Agent
│   ├── market_analyst.py
│   ├── industry_analyst.py
│   ├── company_analyst.py
│   └── critic.py       # 自批评Agent
│
├── tools/              # 工具集
│   ├── data_tools.py   # 数据采集
│   ├── analysis_tools.py # 分析工具
│   └── mcp_tools.py    # MCP集成
│
├── graph/              # LangGraph定义
│   └── research_graph.py
│
├── api/                # FastAPI服务
├── ui/                 # Streamlit界面
└── tests/              # 测试

## 开发计划
### Phase 1: MVP (2周)
- [ ] Agent框架搭建
- [ ] 基础数据采集
- [ ] 单股票研究流程

### Phase 2: 增强 (2周)
- [ ] 多Agent协作
- [ ] RAG增强
- [ ] 自批评机制

### Phase 3: 产品化 (2周)
- [ ] API服务
- [ ] Dashboard
- [ ] 部署上线

## 质量标准
- 测试覆盖率 > 80%
- API响应时间 < 3s
- 研究报告准确率 > 90%
```

## 检查清单

- [ ] 需求完整
- [ ] 架构合理
- [ ] 计划可行
- [ ] 风险可控
- [ ] 质量标准明确
- [ ] 文档完善

## 红牌警告

- 需求不清晰
- 架构过于复杂
- 计划不现实
- 风险未识别
- 质量标准缺失
