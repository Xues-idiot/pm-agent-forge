---
name: engineering-verification-loop
description: Use when building verification and validation loops into development workflows. Covers continuous verification, automated checks, and quality gates.
---

# Verification Loop

验证循环，将验证集成到开发工作流中。

## 何时使用

- 持续集成/持续部署
- 质量门禁
- 自动化检查
- 发布前验证
- 开发流程优化

## 验证循环概念

### 反馈循环

```markdown
## 反馈循环

### 快速反馈
```
编写代码 → 验证 → 反馈 → 修复 → 继续
    ↑__________________|

### 循环原则
- 快速：反馈<10分钟
- 准确：避免误报
- 清晰：明确问题所在
- 可操作：知道如何修复
```

### 验证层次

```markdown
## 验证层次

| 层次 | 时机 | 内容 |
|------|------|------|
| 本地验证 | 编写时 | 语法、类型 |
| 提交验证 | commit时 | lint、单元测试 |
| PR验证 | merge时 | 集成测试、E2E |
| 部署验证 | 发布时 | 冒烟测试 |
| 生产监控 | 运营时 | 错误率、性能 |
```

## 自动化检查

### 检查类型

```markdown
## 检查类型

### 静态检查
| 检查 | 工具 | 速度 |
|------|------|------|
| Lint | ESLint | 快 |
| 类型检查 | TypeScript | 快 |
| 格式化 | Prettier | 快 |

### 动态检查
| 检查 | 工具 | 速度 |
|------|------|------|
| 单元测试 | Vitest | 中 |
| 集成测试 | Jest | 中 |
| E2E测试 | Playwright | 慢 |

### 安全检查
| 检查 | 工具 |
|------|------|
| 依赖漏洞 | npm audit |
| 代码漏洞 | Snyk |
| SAST | SonarQube |
```
```

### 检查配置

```markdown
## 检查配置

### pre-commit hook
```bash
#!/bin/bash
echo "Running pre-commit checks..."

# Lint
npm run lint
if [ $? -ne 0 ]; then
  echo "Lint failed"
  exit 1
fi

# Tests
npm run test
if [ $? -ne 0 ]; then
  echo "Tests failed"
  exit 1
fi

echo "All checks passed"
exit 0
```
```

## 质量门禁

### 门禁设计

```markdown
## 质量门禁

### 门禁节点
```markdown
## 门禁节点

### PR阶段门禁
- [ ] 代码格式通过
- [ ] 类型检查通过
- [ ] 单元测试通过
- [ ] 覆盖率达标(>80%)
- [ ] 安全扫描通过
- [ ] 至少1人审批

### 部署阶段门禁
- [ ] 构建成功
- [ ] E2E测试通过
- [ ] 性能测试达标
- [ ] 配置文件正确
```
```

### 门禁标准

```markdown
## 门禁标准

### 可配置标准
| 指标 | 阈值 | 严重程度 |
|------|------|----------|
| 测试覆盖率 | >80% | Error |
| Bug数量 | 0 | Error |
| 性能回归 | <5% | Warning |
| 安全漏洞 | 0 | Critical |

### 失败处理
```markdown
## 门禁失败

### 策略
- 严重：阻止合并/部署
- 警告：通知但允许
- 信息：记录但不阻止

### 通知
- Slack/飞书通知
- 邮件通知
- 代码审查评论
```
```

## 持续集成

### CI/CD流程

```markdown
## CI/CD流程

### 典型流程
```
代码提交 → 构建 → 测试 → 部署

1. 代码提交到分支
2. CI自动运行检查
3. 通过后合并到主分支
4. CD自动部署到测试环境
5. 人工审批后部署生产
```

### GitHub Actions示例
```yaml
name: CI
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm ci
      - run: npm run lint
      - run: npm run test
      - run: npm run build
```

### GitLab CI示例
```yaml
stages:
  - build
  - test
  - deploy

build:
  stage: build
  script:
    - npm ci
    - npm run build

test:
  stage: test
  script:
    - npm run lint
    - npm run test

deploy:
  stage: deploy
  script:
    - npm run deploy
  only:
    - main
```

## 验证工具

### 工具链

```markdown
## 工具链

### 前端工具链
| 阶段 | 工具 |
|------|------|
| Lint | ESLint, Prettier |
| Type | TypeScript |
| Test | Vitest, Playwright |
| Bundle | Webpack, Vite |
| Deploy | Vercel, Netlify |

### 后端工具链
| 阶段 | 工具 |
|------|------|
| Lint | ESLint, Ruff |
| Type | TypeScript, mypy |
| Test | Jest, Pytest |
| Build | Docker |
| Deploy | K8s, AWS |
```

### 工具配置

```markdown
## 工具配置

### package.json scripts
```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "lint": "eslint . --ext .ts,tsx",
    "format": "prettier --write .",
    "test": "vitest",
    "test:ci": "vitest --run",
    "typecheck": "tsc --noEmit"
  }
}
```
```

## 监控与反馈

### 运行时监控

```markdown
## 运行时监控

### 监控指标
| 指标 | 告警阈值 |
|------|----------|
| 错误率 | >1% |
| 响应时间P99 | >2s |
| CPU使用率 | >80% |
| 内存使用率 | >85% |

### 监控工具
| 工具 | 用途 |
|------|------|
| Sentry | 错误追踪 |
| Datadog | 性能监控 |
| Grafana | 可视化 |
| Prometheus | 指标收集 |
```

### 反馈机制

```markdown
## 反馈机制

### 反馈渠道
| 渠道 | 场景 |
|------|------|
| Slack | 失败通知 |
| 邮件 | 重要告警 |
| Dashboard | 实时状态 |
| 代码评论 | PR审查 |

### 反馈内容
```markdown
## 反馈内容

### 检查失败
- 失败的测试
- 错误信息
- 相关代码位置
- 修复建议

### 性能回归
- 性能对比
- 影响范围
- 可能原因
```
```

## 持续改进

### 指标追踪

```markdown
## 指标追踪

### 过程指标
| 指标 | 目标 |
|------|------|
| 构建时间 | <10分钟 |
| 测试时间 | <5分钟 |
| MTTR | <1小时 |
| 发布频率 | 每周多次 |

### 质量指标
| 指标 | 目标 |
|------|------|
| 缺陷逃逸率 | <5% |
| 自动化覆盖率 | >90% |
| 门禁通过率 | >95% |
```
```

### 优化实践

```markdown
## 优化实践

### 加速检查
- 并行执行测试
- 跳过未修改文件的测试
- 缓存依赖和构建结果

### 减少误报
- 定期审查失败用例
- 修复而非忽略
- 区分环境问题

### 改进门禁
- 从实际故障中学习
- 调整不合理的阈值
- 添加缺失的检查
```

## 检查清单

- [ ] 有完整的验证工具链
- [ ] 门禁标准明确
- [ ] 反馈及时
- [ ] 失败可追踪
- [ ] 持续优化改进
- [ ] 团队遵循流程

## 红牌警告

- 检查过于缓慢
- 误报率过高
- 失败不修复
- 门禁流于形式
- 没有反馈机制
- 不做持续改进