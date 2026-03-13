# 基于 YOLOv5 的火焰检测模型迭代优化实验

> **实验性质**：工程验证 · 迭代优化 · 方法复现  
> 本仓库记录了一次完整的深度学习模型迭代优化过程，旨在验证训练策略对模型性能的影响。原始代码基于 [Ultralytics YOLOv5](https://github.com/ultralytics/yolov5)，遵循 [AGPL-3.0](LICENSE) 协议。

## 实验概述
| 项目 | 说明 |
|------|------|
| **任务** | 火焰与消防车目标检测 |
| **基线模型** | YOLOv5s (预训练权重) |
| **优化策略** | 增加训练轮数 + 早停机制 |
| **评估指标** | 召回率 (Recall), mAP@0.5, 混淆矩阵, 训练曲线 |

## 实验设置
| 阶段 | 训练配置 | 目的 |
|------|----------|------|
| **Baseline** | 训练 100 轮，默认超参数 | 建立性能基线，观察模型初步收敛情况 |
| **Improved** | **设置 300 轮，启用早停（patience=20）**，模型在第 97 轮自动停止 | 验证“充分训练+早停”能否提升模型性能，避免过拟合 |

## 量化结果对比
| 指标 | Baseline (100轮) | Improved (97轮早停) | 相对提升 |
|------|------------------|---------------------|----------|
| **Recall** | 0.37 | 0.45 | **+21.6%** |
| **mAP@0.5** | ~0.31 | ~0.43 | **+38.7%** |

## 可视化证据
### 1. 混淆矩阵对比
- **Baseline**: `![Baseline Confusion](./ARCHIVE/Baseline/baseline_confusion.png)`
- **Improved**: `![Improved Confusion](./ARCHIVE/Improved/improved_confusion.png)`

### 2. 训练曲线对比
- **Baseline**: `![Baseline Training](./ARCHIVE/Baseline/baseline_training.png)`
- **Improved**: `![Improved Training](./ARCHIVE/Improved/improved_training.png)`

### 3. 检测效果对比
- **Baseline**: `![Baseline Detection](./ARCHIVE/Baseline/baseline_detection.png)`
- **Improved**: `![Improved Detection](./ARCHIVE/Improved/improved_detection.png)`

## 结论
通过增加训练轮数并引入早停机制，模型在**召回率和 mAP@0.5 上均获得显著提升**（+21.6% / +38.7%），证明“充分训练+早停”是有效的优化策略。混淆矩阵和训练曲线也验证了模型收敛性更好，误检和漏检减少。检测效果图进一步直观展示了改进后模型在实际场景中的鲁棒性提升。

## 项目结构
