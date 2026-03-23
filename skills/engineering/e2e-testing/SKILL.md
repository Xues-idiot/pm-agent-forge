---
name: engineering-e2e-testing
description: Use when designing and implementing end-to-end tests for applications. Covers E2E testing frameworks, test scenarios, and automation.
---

# E2E Testing

端到端测试，验证整个应用系统的正确性。

## 何时使用

- 核心业务流程测试
- 用户交互验证
- 多系统集成测试
- 回归测试
- 自动化测试

## 测试策略

### 测试金字塔

```markdown
## 测试金字塔

### 分层结构
```
        /\
       /  \      E2E (少量)
      /____\
     /      \    Integration (中量)
    /________\
   /          \   Unit (大量)
  /____________\

数量: 少 → 多
成本: 高 → 低
速度: 慢 → 快
```

### 各层特点
| 层级 | 测试内容 | 数量比例 | 工具 |
|------|----------|----------|------|
| E2E | 整个系统 | 10-20% | Playwright, Cypress |
| Integration | 模块间交互 | 20-30% | Jest, Pytest |
| Unit | 单个函数 | 50-70% | Vitest, JUnit |

### E2E测试场景选择
```markdown
## E2E场景选择

### 适合E2E的场景
- 核心业务流程：登录、支付
- 关键用户路径：下单、注册
- 跨系统交互：API集成
- 复杂UI交互：拖拽、表单

### 不适合E2E的场景
- 边界情况
- 异常处理
- 内部逻辑
- 单元功能
```

## 测试框架

### 框架对比

```markdown
## 测试框架对比

| 框架 | 语言 | 优点 | 缺点 |
|------|------|------|------|
| Playwright | TS/JS | 跨浏览器、自动等待 | 学习曲线 |
| Cypress | JS/TS | 易用、实时reload | 仅支持JS |
| Selenium | 多语言 | 生态大、语言多 | 配置复杂 |
| Puppeteer | JS/TS | Chrome控制 | 仅Chrome |

### Playwright示例
```typescript
import { test, expect } from '@playwright/test';

test('login flow', async ({ page }) => {
  await page.goto('/login');
  await page.fill('[name="email"]', 'test@example.com');
  await page.fill('[name="password"]', 'password');
  await page.click('[type="submit"]');
  await expect(page).toHaveURL('/dashboard');
});
```

### Cypress示例
```javascript
describe('Login', () => {
  it('should login successfully', () => {
    cy.visit('/login');
    cy.get('[name="email"]').type('test@example.com');
    cy.get('[name="password"]').type('password');
    cy.get('[type="submit"]').click();
    cy.url().should('include', '/dashboard');
  });
});
```

## 测试设计

### 测试用例设计

```markdown
## 测试用例设计

### 设计原则
| 原则 | 说明 |
|------|------|
| 独立性 | 测试间不依赖 |
| 可重复 | 多次运行结果一致 |
| 清晰性 | 命名清晰、步骤明确 |
| 原子性 | 一个用例一个验证 |

### 命名规范
```markdown
## 命名规范

### 命名模式
[功能]_[场景]_[预期]

### 示例
login_with_valid_credentials_should_succeed
checkout_with_empty_cart_should_show_error
payment_with_invalid_card_should_fail
```
```

### 测试场景

```markdown
## 测试场景

### 冒烟测试
```markdown
## 冒烟测试

### 核心功能
- 应用能启动
- 核心页面可访问
- 主要流程能走通

### 示例用例
1. 首页加载成功
2. 用户能登录
3. 能看到核心内容
```
```

### 回归测试
```markdown
## 回归测试

### 覆盖范围
- 已有功能未被破坏
- Bug修复未引入新问题
- 性能未明显下降

### 优先级
P0：核心功能
P1：重要功能
P2：次要功能
```
```

### Happy Path vs Edge Cases

```markdown
## 测试路径

### Happy Path
```markdown
## 正常流程

### 步骤
1. 输入正确数据
2. 按预期操作
3. 获得预期结果

### 示例
登录 → 选择商品 → 加入购物车 → 支付 → 订单完成
```
```

### Edge Cases
```markdown
## 边界情况

### 数据边界
- 空输入
- 超长文本
- 特殊字符
- 格式错误

### 状态边界
- 并发操作
- 网络异常
- 超时处理
- 服务不可用
```

## 页面对象模型

### POM模式

```markdown
## Page Object Model

### 概念
页面元素和操作封装为对象

### 示例结构
```typescript
// LoginPage.ts
class LoginPage {
  constructor(page: Page) {
    this.page = page;
  }

  async goto() {
    await this.page.goto('/login');
  }

  get emailInput() {
    return this.page.locator('[name="email"]');
  }

  get passwordInput() {
    return this.page.locator('[name="password"]');
  }

  get submitButton() {
    return this.page.locator('[type="submit"]');
  }

  async login(email: string, password: string) {
    await this.emailInput.fill(email);
    await this.passwordInput.fill(password);
    await this.submitButton.click();
  }
}
```
```

### POM优势
```markdown
## POM优势

### 维护性
- 元素变更只需改一处

### 可读性
- 测试代码更清晰

### 可复用
- 多个测试可共用

### 分层
- 页面逻辑 vs 测试逻辑
```

## 测试数据

### 测试数据管理

```markdown
## 测试数据

### 数据策略
| 策略 | 适用 | 特点 |
|------|------|------|
| 硬编码 | 简单测试 | 快速但不灵活 |
| Fixture | 固定数据 | 可复用 |
| Factory | 动态生成 | 灵活 |
| API调用 | 真实数据 | 真实但慢 |

### Fixture示例
```typescript
// fixtures/user.ts
export const validUser = {
  email: 'test@example.com',
  password: 'password123',
  name: 'Test User',
};

export const adminUser = {
  ...validUser,
  role: 'admin',
};
```

### Factory示例
```typescript
// factories/user.ts
function createUser(overrides = {}) {
  return {
    id: generateId(),
    email: `user${Date.now()}@example.com`,
    password: 'password123',
    ...overrides,
  };
}

// 使用
const user = createUser({ role: 'admin' });
```

## 测试报告

### 报告内容

```markdown
## 测试报告

### 必含内容
| 内容 | 说明 |
|------|------|
| 执行概况 | 通过/失败/跳过 |
| 失败详情 | 错误信息和截图 |
| 执行时间 | 各测试耗时 |
| 覆盖率 | 覆盖的场景 |

### 报告工具
| 工具 | 特点 |
|------|------|
| Allure | 美观、详细 |
| ReportPortal | 集中管理 |
| 内置HTML | 简单项目 |
```

### CI/CD集成

```markdown
## CI/CD集成

### GitHub Actions
```yaml
name: E2E Tests
on: [push, pull_request]

jobs:
  e2e:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run tests
        run: npm test
      - name: Upload screenshots
        if: failure()
        uses: actions/upload-artifact@v2
        with:
          name: test-screenshots
          path: screenshots/
```
```

## 最佳实践

### 测试稳定性

```markdown
## 稳定性实践

### 避免 flaky tests
- 使用显式等待
- 避免time.sleep
- 独立测试数据
- 清理测试状态

### 等待策略
```typescript
// Playwright - 推荐
await expect(page.locator('.success')).toBeVisible({ timeout: 5000 });

// 避免
await page.waitForTimeout(3000); // ❌
```
```

### 并行执行

```markdown
## 并行测试

### 配置
```typescript
// playwright.config.ts
export default {
  fullyParallel: true,
  workers: process.env.CI ? 2 : undefined,
};
```

### 注意事项
- 测试间不共享状态
- 使用独立数据库
- 避免端口冲突
```

## 检查清单

- [ ] 覆盖核心用户路径
- [ ] 使用Page Object模式
- [ ] 测试数据独立
- [ ] 有适当的等待
- [ ] 失败有截图
- [ ] CI/CD集成

## 红牌警告

- 测试过于缓慢
- flaky tests过多
- 测试间相互依赖
- 不清理测试数据
- 元素选择器脆弱
- 不做回归测试