---
name: engineering-documentation-lookup
description: Use when searching, reading, and applying technical documentation. Covers documentation search strategies, reading techniques, and applying information.
---

# Documentation Lookup

文档查询，快速找到和应用技术文档。

## 何时使用

- 查找API用法
- 理解框架用法
- 排查问题
- 学习新技术
- 确认最佳实践

## 搜索策略

### 搜索技巧

```markdown
## 搜索技巧

### 关键词选择
| 策略 | 示例 |
|------|------|
| 核心词 | React useEffect |
| 官方术语 | React Hooks |
| 错误信息 | "Cannot read property" React |
| 版本号 | React 18 |

### 搜索限定
| 限定 | 语法 | 示例 |
|------|------|------|
| 站点 | site: | site:github.com React |
| 文件类型 | filetype: | filetype:pdf API |
| 精确匹配 | " " | "useEffect" cleanup |
| 排除 | - | React -Native |
```
```

### 资源优先级

```markdown
## 资源优先级

### 优先顺序
1. 官方文档（最新、最准）
2. 官方教程/指南
3. 官方API参考
4. 认证课程
5. 知名博客
6. Stack Overflow
7. GitHub Issues
8. 社区讨论

### 官方文档特点
- 最权威
- 更新及时
- 示例完整
- 有中文版（部分）
```

## 文档阅读

### 阅读方法

```markdown
## 文档阅读

### 快速定位
| 目标 | 方法 |
|------|------|
| 找用法 | API参考 |
| 理解概念 | 指南/教程 |
| 解决问题 | FAQ/Troubleshooting |
| 配环境 | Getting Started |

### 深度阅读
```markdown
## 深度阅读

### 步骤
1. 预览：看目录和结构
2. 略读：快速过一遍
3. 精读：重点部分细读
4. 笔记：记录关键点
5. 实践：写代码验证
```
```

### API文档阅读

```markdown
## API文档阅读

### 必看内容
| 部分 | 重要性 |
|------|--------|
| 签名 | 必看 |
| 参数说明 | 必看 |
| 返回值 | 必看 |
| 示例 | 必看 |
| 注意事项 | 推荐 |
| 源码 | 可选 |

### 示例解读
```markdown
## 示例解读

### 代码示例
// 注释说明关键点
const result = api.method(param); // 返回值

### 解读步骤
1. 理解输入参数
2. 理解返回值
3. 理解使用场景
4. 注意边界情况
```
```

## 问题排查

### 排查流程

```markdown
## 问题排查

### 步骤
1. 明确错误信息
2. 搜索错误信息
3. 定位官方文档
4. 查看解决方案
5. 验证修复

### 搜索策略
```markdown
## 错误搜索

### 搜索词组合
"错误信息" + 技术栈
"错误信息" + 版本号
"错误信息" + "solution"
```
```

### 常见问题资源

```markdown
## 问题资源

### 官方资源
| 资源 | 用途 |
|------|------|
| FAQ | 常见问题 |
| Troubleshooting | 故障排查 |
| Changelog | 版本变更 |
| Migration Guide | 迁移指南 |

### 社区资源
| 资源 | 特点 |
|------|------|
| Stack Overflow | 问答多 |
| GitHub Issues | 官方确认 |
| Reddit | 讨论多 |
| Discord | 实时帮助 |
```

## 版本管理

### 多版本文档

```markdown
## 多版本文档

### 常用框架版本策略
| 框架 | 版本策略 |
|------|----------|
| React | 最新稳定版 |
| Vue | 维护多版本 |
| Angular | 保持更新 |
| Node.js | LTS版 |

### 版本选择建议
```markdown
## 版本选择

### 生产环境
- 使用LTS版本
- 参考稳定版文档

### 学习环境
- 可以用最新版
- 参考最新版文档

### 迁移
- 查看Migration Guide
- 逐版本升级
```
```

## 知识管理

### 笔记方法

```markdown
## 知识笔记

### 笔记内容
```markdown
## 技术笔记

### 标题
React useEffect

### 核心要点
1. 副作用钩子
2. 依赖数组控制执行
3.  cleanup函数

### 示例代码
```jsx
useEffect(() => {
  // effect
  return () => {}; // cleanup
}, [deps]);
```

### 注意事项
- 空依赖数组只在首次执行
- 依赖要完整
```
```

### 知识库组织

```markdown
## 知识库组织

### 分类方式
- 按技术栈：React/Vue/Angular
- 按类型：用法/问题/最佳实践
- 按场景：入门/进阶/源码

### 工具选择
| 工具 | 适用 |
|------|------|
| Notion | 知识管理 |
| Obsidian | 笔记链接 |
| GitHub | 代码笔记 |
| 语雀 | 团队知识 |
```

## 实践应用

### 文档验证

```markdown
## 文档验证

### 验证方法
1. 运行官方示例
2. 检查版本兼容性
3. 测试边界情况
4. 记录实践经验

### 常见问题
| 问题 | 原因 |
|------|------|
| 示例不运行 | 版本差异 |
| 行为不同 | 理解偏差 |
| API已变 | 文档过时 |
```
```

### 持续学习

```markdown
## 持续学习

### 保持更新
- 订阅官方博客
- 关注Release Notes
- 定期回顾知识

### 学习资源
| 资源 | 频率 |
|------|------|
| 官方博客 | 每周 |
| Release Notes | 按版本 |
| 技术周刊 | 每周 |
| 社区讨论 | 按需 |
```

## 检查清单

- [ ] 搜索策略正确
- [ ] 优先查看官方文档
- [ ] 理解完整再动手
- [ ] 记录关键信息
- [ ] 验证信息准确性
- [ ] 分享给团队

## 红牌警告

- 搜索词不准确
- 迷信非官方文档
- 不验证直接使用
- 不记录易遗忘
- 不更新知识库
- 不分享给团队