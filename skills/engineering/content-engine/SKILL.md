---
name: engineering-content-engine
description: Use when building content management systems, content pipelines, or content processing workflows. Covers content authoring, storage, versioning, and delivery.
---

# Content Engine

内容引擎，构建内容管理系统和处理流水线。

## 何时使用

- CMS系统开发
- 内容平台搭建
- 多渠道内容分发
- 内容工作流
- 内容分析

## 内容模型

### 内容结构

```markdown
## 内容模型

### 内容类型
| 类型 | 说明 | 示例 |
|------|------|------|
| 文章 | 长文本内容 | 博客、新闻 |
| 页面 | 静态页面 | About、帮助 |
| 产品 | 商品信息 | 商品详情 |
| 媒体 | 多媒体 | 图片、视频 |
| 用户 | 用户生成 | 评论、帖子 |

### 字段设计
```markdown
## 字段设计

### 通用字段
| 字段 | 类型 | 说明 |
|------|------|------|
| id | string | 唯一标识 |
| title | string | 标题 |
| slug | string | URL别名 |
| content | text | 正文 |
| status | enum | 状态 |
| createdAt | datetime | 创建时间 |
| updatedAt | datetime | 更新时间 |
| author | relation | 作者 |

### 扩展字段
```markdown
## 扩展字段

### 文章扩展
- summary: 摘要
- coverImage: 封面图
- tags: 标签
- category: 分类
- publishedAt: 发布时间
```
```

### 关系设计

```markdown
## 内容关系

### 关系类型
| 类型 | 说明 | 示例 |
|------|------|------|
| 一对一 | 一个对应一个 | 文章-封面图 |
| 一对多 | 一个对应多个 | 分类-文章 |
| 多对多 | 多个对应多个 | 文章-标签 |

### 实现方式
```markdown
## 关系实现

### 关系表
article_tags:
- article_id
- tag_id

### 嵌套文档
{
  "article": {
    "id": "1",
    "tags": ["tech", "ai"]
  }
}
```
```

## 内容存储

### 存储方案

```markdown
## 存储方案

### 数据库选择
| 数据库 | 适用 | 特点 |
|------|------|------|
| PostgreSQL | 关系型内容 | 结构化、ACID |
| MongoDB | 文档型内容 | 灵活Schema |
| Elasticsearch | 搜索型内容 | 全文搜索 |
| Redis | 缓存热点内容 | 高速读写 |

### 混合存储
```markdown
## 混合存储

### 策略
- PostgreSQL：主数据
- Elasticsearch：搜索索引
- Redis：缓存
- S3：文件存储
```
```

### 版本控制

```markdown
## 版本控制

### 版本策略
```markdown
## 版本实现

### 表结构
article_versions:
- id
- article_id
- version
- title
- content
- created_at
- created_by

### 当前版本
article:
- id
- current_version_id
```
```

## 内容工作流

### 工作流设计

```markdown
## 内容工作流

### 典型流程
```
创建 → 编辑 → 审核 → 发布

1. 起草：内容创建
2. 编辑：内容修改
3. 审核：审核通过/拒绝
4. 发布：上线
5. 归档：下架/存档
```

### 状态机
```markdown
## 状态机

### 状态定义
- draft: 草稿
- pending: 待审核
- approved: 审核通过
- rejected: 审核拒绝
- published: 已发布
- archived: 已归档

### 状态转换
draft → pending → approved → published
draft → rejected
published → archived
```
```

### 权限控制

```markdown
## 权限控制

### 角色权限
| 角色 | 创建 | 编辑 | 审核 | 发布 | 删除 |
|------|------|------|------|------|------|
| 作者 | ✓ | 自己的 | ✗ | ✗ | ✗ |
| 编辑 | ✓ | ✓ | ✗ | ✗ | ✗ |
| 审核 | ✓ | ✓ | ✓ | ✗ | ✗ |
| 管理员 | ✓ | ✓ | ✓ | ✓ | ✓ |
```

## 内容API

### API设计

```markdown
## 内容API

### RESTful设计
| 方法 | 端点 | 说明 |
|------|------|------|
| GET | /articles | 列表 |
| GET | /articles/:slug | 详情 |
| POST | /articles | 创建 |
| PUT | /articles/:id | 更新 |
| DELETE | /articles/:id | 删除 |
| POST | /articles/:id/publish | 发布 |
| POST | /articles/:id/archive | 归档 |

### GraphQL设计
```graphql
type Article {
  id: ID!
  title: String!
  content: String!
  author: Author!
  tags: [Tag!]!
  publishedAt: DateTime
}

type Query {
  articles(filter: ArticleFilter): [Article!]!
  article(slug: String!): Article
}

type Mutation {
  createArticle(input: CreateArticleInput!): Article!
  updateArticle(id: ID!, input: UpdateArticleInput!): Article!
}
```
```

### 查询优化

```markdown
## 查询优化

### N+1问题
```typescript
// 问题
const articles = await db.getArticles();
for (const article of articles) {
  article.author = await db.getAuthor(article.authorId); // N次查询
}

// 解决：预加载
const articles = await db.getArticles().include('author');
```
```

## 多渠道分发

### 分发策略

```markdown
## 多渠道分发

### 渠道类型
| 渠道 | 格式 | 特点 |
|------|------|------|
| Web | HTML | 完整内容 |
| App | JSON | 结构化数据 |
| 小程序 | JSON | 简化内容 |
| 社交 | 短内容 | 摘要+链接 |
| 搜索 | 优化后HTML | SEO友好 |

### 分发流程
```markdown
## 分发流程

源内容 → 格式转换 → 渠道适配 → 发布

1. 源内容统一存储
2. 格式转换为各渠道
3. 根据渠道特性调整
4. 发布到对应平台
```
```

### 模板引擎

```markdown
## 模板引擎

### 常用模板
| 模板 | 用途 | 工具 |
|------|------|------|
| HTML模板 | Web渲染 | EJS, Handlebars |
| Markdown | 文档 | marked |
| Email模板 | 邮件 | MJML |
| PDF模板 | 文档生成 | Puppeteer |

### 示例
```javascript
// Handlebars
const template = Handlebars.compile(`
  <article>
    <h1>{{title}}</h1>
    <img src="{{coverImage}}" />
    <div class="content">{{{content}}}</div>
  </article>
`);

const html = template({
  title: '文章标题',
  coverImage: '/img/cover.jpg',
  content: '<p>正文内容</p>'
});
```
```

## 内容分析

### 分析指标

```markdown
## 内容分析

### 消费指标
| 指标 | 计算 | 意义 |
|------|------|------|
| PV | 页面浏览 | 曝光 |
| UV | 独立访问 | 触达 |
| 阅读率 | 阅读完整/打开 | 内容质量 |
| 互动率 | 互动/曝光 | 参与度 |

### 质量指标
| 指标 | 计算 | 意义 |
|------|------|------|
| 分享率 | 分享/阅读 | 内容价值 |
| 评论率 | 评论/阅读 | 参与度 |
| 收藏率 | 收藏/阅读 | 长期价值 |

### 转化指标
```markdown
## 转化分析

### 漏斗
阅读 → 感兴趣 → 行动 → 转化

### 追踪内容
- CTA点击率
- 注册转化
- 购买转化
- 留资转化
```
```

## 缓存策略

### 缓存设计

```markdown
## 缓存策略

### 缓存层级
| 层级 | 内容 | TTL |
|------|------|-----|
| CDN | 静态资源 | 1天+ |
| 边缘缓存 | 热门内容 | 1小时 |
| 应用缓存 | 热点内容 | 5-15分钟 |
| 数据库 | 查询结果 | 1-5分钟 |

### 缓存失效
```markdown
## 失效策略

### 主动失效
- 内容更新时删除缓存
- 标签变更时清除相关缓存

### TTL失效
- 根据内容更新频率设置
- 热门内容短TTL
```
```

## 检查清单

- [ ] 内容模型设计合理
- [ ] 版本控制完善
- [ ] 工作流清晰
- [ ] API设计规范
- [ ] 多渠道适配
- [ ] 分析指标完善

## 红牌警告

- Schema设计混乱
- 缺少版本控制
- 工作流不清晰
- 不考虑扩展性
- 忽视SEO
- 性能问题