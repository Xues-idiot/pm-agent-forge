# 音频增强 (Audio Enhancement)

## Overview

音频增强是提升播客音频质量的技能。包括降噪、均衡、响度标准化等。

## 何时使用

- 原始音频质量差
- 降噪处理
- 音质标准化
- 多轨混音

## 流程

1. **音频分析**：分析音频质量
2. **降噪处理**：去除背景噪音
3. **均衡调节**：调节频谱
4. **响度标准化**：标准化响度
5. **质量检测**：检测处理后质量
6. **格式转换**：转换目标格式
7. **存储管理**：存储处理后音频

## 模板

### 音频增强配置
```python
AUDIO_ENHANCEMENT_CONFIG = {
    "noise_reduction": {
        "level": "medium",
        "sample_rate": 48000
    },
    "eq": {
        "low_cut": 80,  # Hz
        "high_cut": 16000,  # Hz
        "presets": "podcast"
    },
    "loudness": {
        "target": -16,  # LUFS
        "true_peak": -1  # dB
    }
}

async def enhance_audio(input_path: str, output_path: str) -> EnhancedAudio:
    """增强音频"""
    # 加载音频
    audio = await load_audio(input_path)

    # 降噪
    denoised = await reduce_noise(audio, level="medium")

    # 均衡
    eqed = await apply_eq(denoised, preset="podcast")

    # 响度标准化
    normalized = await normalize_loudness(eqed, target=-16)

    # 保存
    await save_audio(normalized, output_path)

    return EnhancedAudio(
        path=output_path,
        quality_score=calculate_quality_score(normalized),
        noise_reduction_applied=True,
        loudness=calculate_loudness(normalized)
    )
```

## 检查清单

- [ ] 降噪有效
- [ ] 音质保持
- [ ] 响度标准
- [ ] 无失真
- [ ] 格式正确
- [ ] 质量达标

## 红牌警告

- 降噪过度
- 音质损失
- 失真
- 响度不标准
- 格式问题
