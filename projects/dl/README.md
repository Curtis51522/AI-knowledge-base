---
tags:
  - dl
  - oct
  - assignment
  - convnext
  - swin
  - research
  - paper
date: 2026-06-24
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

## 🎯 期刊投稿路线图

### 推荐期刊：IJIST（International Journal of Imaging Systems and Technology）
| 项目 | 值 |
|------|-----|
| **中科院大类（计算机科学）** | **3区** |
| **中科院小类（工程电子电气）** | **3区** |
| JCR 分区 | Q3 |
| 影响因子 | 3.0 |
| 审稿周期 | ~3个月 |
| 录用比例 | 容易 |

### 其他候选
- JMIHI（Journal of Medical Imaging and Health Informatics）— Q3，但声誉一般
- IET Image Processing — Q3，竞争更大

### 当前状态的差距

| 维度 | 差距 | 严重度 |
|------|------|--------|
| 方法创新 | 零创新，纯对比工作 | 🔴 致命 |
| 泛化验证 | 只用了 Kermany 一个数据集 | 🔴 致命 |
| Baseline 完整性 | 只有 ConvNeXt 和 Swin，缺 ResNet50/EfficientNet/ViT | 🟡 重要 |
| 统计严谨性 | 无重复 seed、无置信区间、无显著性检验 | 🟡 重要 |
| 医学合作者 | 无医生，Discussion 缺临床洞察 | 🟡 重要 |
| 写作 | 课程报告长度 + 文献综述深度不足 | 🟢 可加 |

### 必须补的三件事
1. **加第二个数据集**（OCTID ~500张 或 Duke DME）做 zero-shot 跨域验证
2. **补 baseline**：ResNet50+SE、EfficientNet-B3、ViT-Base/16，跑 3 次 seed 出 mean±std
3. **增量创新**：把互补性错例 → Class-Adaptive EMA（见 `DL/notebook/class_adaptive_ema.py`）

### 实验计划
```
主实验:   Kermany OCT2017 原始83K → 跟前人论文公平对比
验证泛化: OCTID / Duke DME       → zero-shot 推理
副实验:   V2 清洗版 29K          → 展示去重+清洗对结果的提升
```

### 审稿人最可能的拒稿理由（按概率）
1. **缺乏方法创新** (70%) — 纯应用没改进
2. **数据集单一** (60%) — 单数据集泛化性存疑
3. **统计不充分** (50%) — 无重复 seed 和置信区间
4. **医学意义缺失** (40%) — Discussion 深度不够
5. **文献引用不足** (30%) — 需补近 3 年 SOTA 对比

### 诚实评估
- 当前状态直接投 Q3：成功率 <5%
- 补完增量任务后投 IJIST：成功率 ~40-50%
- 最大卖点：CNN-Transformer 互补错误 + Class-Adaptive EMA

---

## 📂 文件位置

| 内容 | 路径 |
|---|---|
| Notebook | `C:\Users\Curtis\Desktop\learningmaterials\SEMESTER3\DL\notebook\final.ipynb` |
| 数据集构建 | `C:\Users\Curtis\Desktop\learningmaterials\SEMESTER3\DL\scripts\build_dataset.py` |
| 训练输出 | `notebook/outputs/` (.pth / .json / .png) |
| Grid Search | `notebook/outputs/grid_search.json` |
| 最终指标 | `notebook/outputs/metrics.json` |
| Class-Adaptive EMA | `notebook/class_adaptive_ema.py` |

---

## ☑️ 待办

- [ ] Grid Search 跑完（20-epoch × 12 组，~4-5h GPU） 🔄
- [ ] 主实验用原始 OCT2017 83K 重跑
- [ ] 跑 Class-Adaptive EMA（已有代码 + 已有 checkpoint → ~5 分钟出结果）
- [ ] 下载 OCTID 做跨域泛化验证
- [ ] 补 baseline：ResNet50+SE、EfficientNet-B3、ViT-Base
- [ ] 跑 3×seed + 统计检验（mean±std + McNemar）
- [ ] 撰写 Word 报告（APU 格式：TNR 12pt, 1.5 倍行距）
- [ ] IJIST 格式短论文（5-6页）
- [ ] 提交：`final.ipynb`（含全部输出）+ Word 报告 + 期刊论文
