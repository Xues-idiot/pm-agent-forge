---
name: data-analytics-visualization-creation
description: Use when creating charts, graphs, dashboards, or any data visualizations for reports and presentations.
---

# Data Analytics Visualization Creation Skill

创建有效的数据可视化，让数据讲故事。

## 何时使用

- 需要将数据可视化
- 创建报表或仪表盘
- 准备演示材料
- 探索性数据分析
- 展示趋势和对比

## 可视化创建流程

```
1. 理解目标 → 2. 选择图表 → 3. 准备数据 → 4. 创建图表 → 5. 美化优化 → 6. 审查输出
```

### 1. 理解目标

**可视化目标：**

| 目标类型 | 描述 | 常用图表 |
|---------|------|---------|
| 趋势 | 随时间变化 | 折线图 |
| 比较 | 不同类别对比 | 柱状图 |
| 构成 | 部分占整体比例 | 饼图、堆叠图 |
| 分布 | 数据分布情况 | 直方图、箱线图 |
| 关系 | 两变量关系 | 散点图 |
| 排名 | 从高到低排序 | 条形图 |

### 2. 选择图表

**图表选择指南：**

```markdown
## 图表选择

### 比较关系
✓ 柱状图：离散的类别对比
✓ 条形图：排名展示
✓ 堆叠图：部分vs整体+对比

### 趋势关系
✓ 折线图：时间序列
✓ 面积图：强调幅度

### 构成关系
✓ 饼图：简单的部分vs整体（<6类）
✓ 堆叠柱状图：随时间变化的构成
✓ 瀑布图：构成分解

### 分布关系
✓ 直方图：单变量分布
✓ 箱线图：分布统计
✓ 散点图：两变量关系

### 地理数据
✓ 地图热力图：地区分布
✓ 气泡图：多维数据
```

### 3. 准备数据

**数据准备清单：**

```markdown
## 数据准备

### 数据格式
- 长格式 vs 宽格式
- 是否需要聚合
- 是否需要排序

### 数据清洗
- [ ] 去除异常值（如需要）
- [ ] 计算百分比（如需要）
- [ ] 排序（如需要）
```

### 4. 创建图表

**基础图表模板：**

```python
import matplotlib.pyplot as plt
import seaborn as sns

# 柱状图
plt.figure(figsize=(10, 6))
sns.barplot(x='类别', y='数值', data=df)
plt.title('标题')
plt.xlabel('X轴标签')
plt.ylabel('Y轴标签')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# 折线图
plt.figure(figsize=(12, 6))
sns.lineplot(x='日期', y='数值', data=df, marker='o')
plt.title('趋势')
plt.grid(True)
plt.show()
```

```javascript
// ECharts 示例
option = {
    title: { text: '标题' },
    tooltip: { trigger: 'axis' },
    legend: { data: ['系列1', '系列2'] },
    xAxis: { type: 'category', data: ['类别1', '类别2'] },
    yAxis: { type: 'value' },
    series: [
        { name: '系列1', type: 'bar', data: [120, 200] },
        { name: '系列2', type: 'bar', data: [80, 150] }
    ]
};
```

### 5. 美化优化

**视觉优化指南：**

| 要素 | 建议 |
|------|------|
| 颜色 | ≤7色，使用品牌色或调色板 |
| 标题 | 清晰描述图表主题 |
| 标签 | 避免重叠，可旋转 |
| 图例 | 位置合适，不遮挡数据 |
| 网格 | 浅色辅助线 |
| 宽高比 | 考虑展示场景 |

**配色建议：**

```markdown
## 配色方案

### 专业风格
- 主色：#2E86AB（蓝）
- 辅色：#A23B72（紫）
- 强调：#F18F01（橙）
- 背景：#FFFFFF

### 数据可视化配色
- 连续：渐变蓝/橙
- 分类：调色板彩虹色
- 正负：蓝色(正) / 红色(负)
```

### 6. 审查输出

**审查清单：**

```markdown
## 可视化审查

### 准确性
- [ ] 数据与图表匹配
- [ ] 坐标轴刻度合理
- [ ] 无扭曲展示

### 可读性
- [ ] 标题清晰
- [ ] 标签可读
- [ ] 无遮挡重叠

### 有效性
- [ ] 图表类型合适
- [ ] 趋势/对比清晰
- [ ] 结论显而易见
```

## 常见图表代码模板

### 折线图（趋势）

```python
import pandas as pd
import matplotlib.pyplot as plt

def create_line_chart(df, x_col, y_cols, title, xlabel, ylabel, filename=None):
    """创建折线图"""
    plt.figure(figsize=(12, 6))

    for col in y_cols:
        plt.plot(df[x_col], df[col], marker='o', label=col)

    plt.title(title, fontsize=14)
    plt.xlabel(xlabel, fontsize=12)
    plt.ylabel(ylabel, fontsize=12)
    plt.legend()
    plt.grid(True, alpha=0.3)
    plt.xticks(rotation=45)
    plt.tight_layout()

    if filename:
        plt.savefig(filename, dpi=300)
    plt.show()
```

### 柱状图（对比）

```python
def create_bar_chart(df, x_col, y_col, title, xlabel, ylabel, filename=None):
    """创建柱状图"""
    plt.figure(figsize=(10, 6))

    colors = plt.cm.Set3(range(len(df)))
    plt.bar(df[x_col], df[y_col], color=colors)

    plt.title(title, fontsize=14)
    plt.xlabel(xlabel, fontsize=12)
    plt.ylabel(ylabel, fontsize=12)
    plt.xticks(rotation=45, ha='right')

    # 添加数值标签
    for i, v in enumerate(df[y_col]):
        plt.text(i, v + max(df[y_col]) * 0.01, str(v), ha='center')

    plt.tight_layout()
    if filename:
        plt.savefig(filename, dpi=300)
    plt.show()
```

### 饼图（构成）

```python
def create_pie_chart(df, labels, sizes, title, filename=None):
    """创建饼图"""
    plt.figure(figsize=(10, 8))

    colors = plt.cm.Pastel1(range(len(labels)))
    explode = [0.05] * len(labels)  # 突出显示

    plt.pie(sizes, explode=explode, labels=labels, colors=colors,
            autopct='%1.1f%%', shadow=True, startangle=90)
    plt.title(title, fontsize=14)
    plt.axis('equal')

    plt.tight_layout()
    if filename:
        plt.savefig(filename, dpi=300)
    plt.show()
```

## 可视化检查清单

- [ ] 图表类型正确
- [ ] 数据准确无误
- [ ] 标题清晰
- [ ] 标签完整
- [ ] 配色协调
- [ ] 无视觉偏差
- [ ] 适合目标媒体

## 红牌警告

- 饼图超过 7 个分类
- Y 轴不从 0 开始（柱状图）
- 使用 3D 图表造成视觉扭曲
- 颜色难以区分（色盲不友好）
- 截断趋势线误导
- 同时展示太多数据系列
- 图表与数据不一致
