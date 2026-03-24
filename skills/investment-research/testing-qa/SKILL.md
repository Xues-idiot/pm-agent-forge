# 测试与质量保证 (Testing & QA)

## Overview

测试与质量保证是建立投研Agent测试体系的技能。参考FinSight的Pytest实践，确保系统质量。

## 何时使用

- 单元测试
- 集成测试
- API测试
- 回归测试

## 流程

1. **测试策略**：制定测试策略
2. **测试设计**：设计测试用例
3. **框架搭建**：搭建测试框架
4. **用例编写**：编写测试用例
5. **CI集成**：集成CI/CD
6. **测试执行**：执行测试
7. **缺陷管理**：管理缺陷

## 模板

### 测试模板
```python
import pytest
from unittest.mock import Mock, patch

class TestStockDataCollection:
    """股票数据采集测试"""

    def test_fetch_price_success(self):
        """测试成功获取股价"""
        with patch('yfinance.download') as mock_download:
            mock_download.return_value = pd.DataFrame({
                'Close': [180.5, 182.3],
                'Volume': [1000000, 1200000]
            })
            result = fetch_price('600519', '2024-01-01', '2024-01-05')
            assert result is not None
            assert len(result) == 2

    def test_fetch_price_error(self):
        """测试获取股价失败"""
        with patch('yfinance.download', side_effect=Exception("API Error")):
            with pytest.raises(Exception):
                fetch_price('INVALID', '2024-01-01', '2024-01-05')

class TestFinancialAnalysis:
    """财务分析测试"""

    def test_calculate_roe(self):
        """测试ROE计算"""
        data = {'net_profit': 100, 'equity': 1000}
        roe = calculate_roe(data)
        assert roe == 0.1  # 10%

    def test_detect_financial_risk(self):
        """测试财务风险检测"""
        data = {
            'receivables_growth': 0.5,  # 应收款增长50%
            'inventory_growth': 0.6     # 存货增长60%
        }
        risks = detect_financial_risk(data)
        assert 'receivables_anomaly' in risks
```

## 检查清单

- [ ] 测试覆盖完整
- [ ] 用例设计合理
- [ ] 断言准确
- [ ] 隔离有效
- [ ] CI/CD集成
- [ ] 缺陷跟踪

## 红牌警告

- 测试覆盖不足
- 断言不准确
- 测试相互依赖
- 忽略边界情况
- CI/CD失败未修复
