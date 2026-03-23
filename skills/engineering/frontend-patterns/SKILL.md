---
name: engineering-frontend-patterns
description: Use when building frontend applications, choosing UI frameworks, or implementing frontend architecture. Covers component design, state management, and performance optimization.
---

# Frontend Patterns

前端设计模式，构建现代前端应用。

## 何时使用

- 前端架构设计
- 组件设计
- 状态管理
- 性能优化
- 框架选择

## 组件设计

### 组件原则

```markdown
## 组件设计原则

### 单一职责
一个组件只做一件事

### 可复用
- 通用组件：按钮、输入框、卡片
- 业务组件：用户卡片、订单列表

### 纯组件
- 同样的props输出同样的UI
- 不产生副作用
- 易于测试
```

### 组件结构

```markdown
## 组件结构

### 推荐结构
```
Component/
├── index.tsx          # 导出
├── Component.tsx      # 主组件
├── Component.styles.ts # 样式
├── Component.test.tsx  # 测试
└── types.ts           # 类型
```

### Props设计
```typescript
// 好的Props设计
interface ButtonProps {
  variant: 'primary' | 'secondary' | 'ghost';
  size: 'sm' | 'md' | 'lg';
  disabled?: boolean;
  loading?: boolean;
  onClick?: () => void;
  children: React.ReactNode;
}
```

## 状态管理

### 状态类型

```markdown
## 状态类型

### UI状态
| 状态 | 说明 |
|------|------|
| isLoading | 加载状态 |
| isOpen | 展开/收起 |
| selected | 选中状态 |
| error | 错误状态 |

### 数据状态
| 状态 | 说明 |
|------|------|
| data | 请求数据 |
| loading | 加载状态 |
| error | 错误信息 |
| pagination | 分页信息 |

### 全局状态
| 状态 | 说明 |
|------|------|
| user | 用户信息 |
| theme | 主题 |
| language | 语言 |
| token | 认证Token |
```

### 状态管理方案

```markdown
## 状态管理方案

### 本地状态
- React: useState
- Vue: ref/reactive

### 跨组件
- React: Context
- Vue: provide/inject

### 全局状态
| 方案 | 适用 |
|------|------|
| Redux | 大型复杂应用 |
| Zustand | 轻量级 |
| Jotai | 原子化 |
| Vuex/Pinia | Vue应用 |
```

### 状态设计原则

```markdown
## 状态设计原则

### 原则
1. 最小化状态
2. 避免派生状态
3. 状态不可变
4. 单一数据源

### 反模式
- 派生数据放状态
- 重复状态
- 模糊状态命名
```

## 数据获取

### 数据获取模式

```markdown
## 数据获取

### 服务端状态
```typescript
// React Query / SWR
const { data, isLoading, error } = useQuery({
  queryKey: ['users'],
  queryFn: fetchUsers,
});
```

### 直接请求
```typescript
// useEffect + useState
const [data, setData] = useState(null);

useEffect(() => {
  fetch('/api/users')
    .then(res => res.json())
    .then(setData);
}, []);
```
```

### 缓存策略

```markdown
## 缓存策略

### 缓存时间
| 数据类型 | 缓存时间 |
|----------|----------|
| 用户数据 | 5-15分钟 |
| 列表数据 | 1-5分钟 |
| 静态数据 | 1小时+ |
| 实时数据 | 不缓存 |

### 缓存更新
- 后台刷新
- 乐观更新
- 失效策略
```

## 性能优化

### 渲染优化

```markdown
## 渲染优化

### React优化
| 优化 | 方式 |
|------|------|
| React.memo | 避免不必要的重渲染 |
| useMemo | 缓存计算结果 |
| useCallback | 缓存回调函数 |
| 虚拟列表 | 长列表优化 |

### Vue优化
| 优化 | 方式 |
|------|------|
| v-memo | 缓存模板 |
| computed | 缓存计算 |
| v-show vs v-if | 控制渲染 |
| 虚拟滚动 | 长列表优化 |
```

### 加载优化

```markdown
## 加载优化

### 代码分割
```javascript
// React.lazy
const HeavyComponent = React.lazy(() => import('./HeavyComponent'));
```

### 图片优化
- 懒加载
- 响应式图片
- WebP格式
- 渐进式加载

### 预加载
```html
<link rel="preload" href="main.js">
<link rel="prefetch" href="next-page.js">
```
```

## CSS模式

### CSS方法论

```markdown
## CSS方法论

### BEM
```css
.block {}
.block__element {}
.block--modifier {}
```

### CSS Modules
```css
/* Button.module.css */
.button {}
.primary {}
```

### Tailwind
```html
<button class="px-4 py-2 bg-blue-500 text-white rounded">
  按钮
</button>
```
```

### 组件样式隔离

```markdown
## 样式隔离

### Shadow DOM
```javascript
const shadow = element.attachShadow({ mode: 'open' });
shadow.innerHTML = '<style>.button { color: blue; }</style>';
```

### CSS-in-JS
```typescript
// styled-components
const Button = styled.button`
  color: blue;
`;
```
```

## 表单处理

### 表单模式

```markdown
## 表单处理

### 受控vs非受控
```typescript
// 受控组件
const [value, setValue] = useState('');
<input value={value} onChange={e => setValue(e.target.value)} />

// 非受控组件
const ref = useRef<HTMLInputElement>(null);
<input defaultValue="init" ref={ref} />
```

### 表单验证
```typescript
// Zod
const schema = z.object({
  email: z.string().email(),
  password: z.string().min(8),
});
```
```

## 错误处理

### 错误边界

```markdown
## 错误边界

### React
```typescript
class ErrorBoundary extends React.Component {
  state = { hasError: false };

  static getDerivedStateFromError() {
    return { hasError: true };
  }

  componentDidCatch(error, info) {
    logError(error, info);
  }

  render() {
    if (this.state.hasError) {
      return <FallbackUI />;
    }
    return this.props.children;
  }
}
```
```

### 全局错误处理

```markdown
## 全局错误处理

### 异步错误
```typescript
window.addEventListener('unhandledrejection', event => {
  logError(event.reason);
});
```

### 请求错误
```typescript
axios.interceptors.response.use(
  response => response,
  error => {
    if (error.response?.status === 401) {
      // 处理未授权
    }
    return Promise.reject(error);
  }
);
```
```

## 检查清单

- [ ] 组件设计合理
- [ ] 状态管理清晰
- [ ] 数据获取规范
- [ ] 性能优化到位
- [ ] 错误处理完善
- [ ] 样式隔离良好

## 红牌警告

- 状态管理混乱
- Props层层传递
- 不做性能优化
- 忽略错误处理
- 全局样式污染
- 不做代码分割