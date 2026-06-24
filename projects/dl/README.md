---
tags:
  - dl
  - oct
  - assignment
  - convnext
  - swin
  - research
  - paper
date: 2026-06-23
status: in-progress
---

# DL Assignment: OCT Retinal Classification — ConvNeXt vs Swin-Tiny

> **CT100-3-M-DL | APU | 四分类：CNV / DME / DRUSEN / NORMAL**
> 数据集：Kermany et al. (2018), Cell — OCT2017_30K_V2（29,408 张清洗后子集）

---

## 🎯 最终结果速查

| | ConvNeXt Base | ConvNeXt +EMA | Swin Base | Swin +EMA |
|---|---|---|---|---|
| Test Acc | 96.37% | 96.44% | 95.87% | **96.03%** |
| Macro F1 | 96.37% | 96.44% | 95.87% | 96.02% |
| AUC | 99.66% | 99.76% | 99.57% | 99.64% |
| Best Val | 97.12% (ep18) | — | 97.28% (ep29) | — |
| Params | 87.5M | — | 27.5M | — |
| Speed | ~5.8 ms/img | — | ~5.2 ms/img | — |

> [!NOTE] Swin vs ConvNeXt gap: 0.41%（从旧版 0.97% 缩小）。数据增强是 Swin 最有效的单一改进（+0.81%）。

---

## 🏗️ 模型配置（Grid Search 最优）

```
Grid Search: lr {1e-3,1e-4,1e-5} × bs {16,32} × wd {1e-3,1e-4} × 20 epochs = 12 组/模型

ConvNeXt 最优: lr=1e-4, bs=32, wd=1e-4
Swin 最优:    lr=1e-4, bs=16, wd=1e-4
```

| 训练设置 | ConvNeXt | Swin-Tiny |
|---|---|---|
| Optimizer | AdamW | AdamW |
| Scheduler | CosineAnnealingLR | Linear warmup(3ep) → Cosine |
| EMA | ✅ decay=0.9999 | ✅ decay=0.9999 |
| Grad Clip | ❌ | ✅ 5.0 |
| AMP | ✅ | ✅ |
| Early Stop | patience=5 | patience=5 |
| Class Weights | ✅ balanced | ✅ balanced |
| Augmentation | RandomHFlip+Rot+ColorJitter+Affine+Erasing | 同 |

---

## 🔑 关键发现（Discussion 直接可用）

### 1. EMA 的类间 tradeoff（临床意义重大）
- ConvNeXt EMA 用 **CNV -3.0%** 换了 DRUSEN +2.0%
- CNV 漏诊 = 延迟抗 VEGF 注射 = 不可逆视力丧失
- **ConvNeXt Base（无 EMA）是临床最优模型**，尽管 total acc 不是最高

### 2. 数据增强对 Transformer 是关键
- Swin 从 95.06% → 95.87%（+0.81%），ConvNeXt 几乎不变
- RandomAffine + RandomErasing 模拟 OCT 的 speckle 噪声和成像偏移
- CNN 自带归纳偏置 → 天生正则化；Transformer 需要显式正则化

### 3. DRUSEN 是全局瓶颈
- 所有模型 DRUSEN ≤ 94%（ConvNeXt Base: 93.9%, Swin Base: 92.4%）
- DRUSEN 特征：微小 RPE 隆起，无液体积聚，极易与 CNV 混淆
- 改进方向：高分辨率输入（384²）、多尺度特征融合（FPN）

### 4. Freeze 深度：小样本 ≠ 全量（方法学贡献）
- 2000 样本消融：freeze=2 最优（+0.86%）
- 25K 全量验证：freeze=0 胜出（-1.58% vs freeze=2）
- **消融结论不能线性外推** — 文献中少有人报告这一现象

### 5. Focal Loss (γ=2) 反降
- Swin 从 95.06% → 94.62%（-0.44%）
- γ=2 过度压制易分样本（CNV/DME/NORMAL），75% 的梯度被浪费
- 不是你参数调错了，是医学四分类不适合高 γ

### 6. CNN-Transformer 互补
- ConvNeXt EMA 错 114 例，Swin EMA 错 127 例，仅 81 例重叠
- Ensemble（简单投票）理论可到 ~97.2% — 零额外训练成本

---

## 📂 文件位置

| 内容 | 路径 |
|---|---|
| Notebook | `C:\Users\Curtis\Desktop\learningmaterials\SEMESTER3\DL\notebook\final.ipynb` |
| 数据集构建 | `C:\Users\Curtis\Desktop\learningmaterials\SEMESTER3\DL\scripts\build_dataset.py` |
| 训练输出 | `notebook/outputs/` (.pth / .json / .png) |
| Grid Search | `notebook/outputs/grid_search.json` |
| 最终指标 | `notebook/outputs/metrics.json` |

---

## ☑️ 待办

- [ ] Grid Search 跑完（20-epoch × 12 组，~4-5h GPU） 🔄
- [ ] Cell 1→17 全量 rerun 确认最终数字
- [ ] 撰写 Word 报告（APU 格式：TNR 12pt, 1.5 倍行距）
- [ ] Literature Review: 引用 Kermany 2018, Isztl 2025, Han 2025
- [ ] Discussion: 合成 6 个关键发现为连贯叙事
- [ ] 提交：`final.ipynb`（含全部输出）+ Word 报告
- [ ] （可选）期刊扩展：384² 分辨率、FPN 多尺度、外部数据集验证
