# 表单自动化 (Form Automation)

## Overview

表单自动化是智能填写和提交换单的技能。

## 何时使用

- 多网站注册
- 批量数据录入
- 问卷调查
- 申请流程

## 流程

1. **表单分析**：分析表单结构
2. **字段映射**：映射数据到字段
3. **智能填写**：AI辅助填写
4. **验证处理**：处理表单验证
5. **验证码处理**：处理验证码
6. **提交执行**：提交表单
7. **结果记录**：记录提交结果

## 模板

### 表单自动化模板
```python
async def auto_fill_form(url: str, form_data: dict):
    """自动填写表单"""
    await page.goto(url)
    await page.wait_for_selector("form")

    for field_name, value in form_data.items():
        # 定位字段
        field = await page.locate_field(field_name)

        if field.type == "text":
            await field.fill(value)
        elif field.type == "select":
            await field.select(value)
        elif field.type == "checkbox":
            if value:
                await field.check()
        elif field.type == "captcha":
            # AI识别验证码
            captcha_text = await solve_captcha(field)
            await field.fill(captcha_text)

    # 提交
    await page.click("[type=submit]")
    await page.wait_for_navigation()

    return {"status": "success", "url": page.url}
```

## 检查清单

- [ ] 定位准确
- [ ] 填写正确
- [ ] 验证处理
- [ ] 验证码处理
- [ ] 提交成功
- [ ] 结果正确

## 红牌警告

- 字段定位失败
- 填写错误
- 验证不通过
- 验证码失败
- 提交失败
- 数据丢失
