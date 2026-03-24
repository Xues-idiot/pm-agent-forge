# 数据可视化 (Data Visualization)

## Overview

数据可视化是将投研数据转化为直观图表的技能。提升研究报告的可读性和说服力。

## 何时使用

- 制作投研图表
- 展示数据趋势
- 对比分析展示
- 制作Dashboard

## 流程

1. **需求分析**：确定可视化目标
2. **数据准备**：准备数据
3. **图表选择**：选择合适的图表
4. **图表制作**：制作图表
5. **美化优化**：优化外观
6. **交互设计**：添加交互
7. **发布部署**：发布图表

## 模板

### 可视化配置模板
```python
import matplotlib.pyplot as plt
import seaborn as sns

# 风格设置
plt.style.use('seaborn-v0_8-whitegrid')
plt.rcParams['font.sans-serif'] = ['SimHei', 'Arial']
plt.rcParams['axes.unicode_minus'] = False

# K线图
def plot_kline(data, title="K线图"):
    fig, ax = plt.subplots(figsize=(12, 6))
    # 绘制K线
    ax.plot(data.index, data['close'])
    ax.set_title(title)
    return fig

# 财务指标对比
def plot_financial_compare(companies, metrics):
    df = pd.DataFrame(metrics, index=companies)
    df.T.plot(kind='bar', figsize=(12, 6))
    plt.title('财务指标对比')

# 组合持仓
def plot_portfolio(allocation):
    labels = list(allocation.keys())
    sizes = list(allocation.values())
    plt.pie(sizes, labels=labels, autopct='%1.1f%%')
    plt.axis('equal')
```

## 检查清单

- [ ] 图表选择合适
- [ ] 数据准确
- [ ] 标注清晰
- [ ] 配色专业
- [ ] 交互流畅
- [ ] 导出方便

## 红牌警告

- 图表误导
- 数据错误
- 配色混乱
- 信息过载
- 缺乏标注
