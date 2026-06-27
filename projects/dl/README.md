---
tags:
  - dl
  - oct
  - assignment
  - convnext
  - swin
  - research
  - paper
date: 2026-06-26
status: complete ✅
---

# DL Assignment: OCT Retinal Classification — ConvNeXt vs Swin-Tiny

> **CT100-3-M-DL | APU | 四分类：CNV / DME / DRUSEN / NORMAL**
> 数据集：Kermany et al. (2018), Cell — OCT2017_30K_V2（29,408 张清洗后子集）

---

## 🎯 最终结果速查

| | ConvNeXt Base | ConvNeXt +EMA 🥇 | Swin Base | Swin +EMA 🥉 |
|---|---|---|---|---|---|
| Test Acc | 96.37% | **97.09%** | 95.62% | **96.19%** |
| Macro F1 | 96.37% | 97.09% | 95.61% | 96.18% |
| AUC | 99.60% | 99.74% | 99.55% | 99.65% |
| Best Val | 97.44% (ep21) | — | 97.60% (ep42) | — |
| Params | 87.5M | — | 27.5M | — |
| Speed | 7.51 ms/img | — | 5.34 ms/img | — |

> [!NOTE] ConvNeXt +EMA 97.09% 🥇 | Swin +EMA 96.19% | Gap: 0.90%。
> 两个模型均通过 Grid Search + EMA + 增强 + stochastic depth 从初始基线大幅提升。

---

## 🏗️ 模型配置（Grid Search 最优）

```
Grid Search: lr {1e-3,1e-4,1e-5} × bs {16,32} × wd {1e-3,1e-4} × 20 epochs = 12 组/模型

ConvNeXt 最优: lr=1e-4, bs=16, wd=1e-3 → val_acc=97.86% (但最终 bs=32 更优)
Swin 最优:    lr=1e-4, bs=32, wd=1e-4 → val_acc=97.14%
```

| 训练设置 | ConvNeXt | Swin-Tiny |
|---|---|---|
| Optimizer | AdamW | AdamW |
| Scheduler | CosineAnnealingLR | Linear warmup(3ep) → Cosine |
| EMA | ✅ decay=0.9999 | ✅ decay=0.9999 |
| Grad Clip | ❌ | ✅ 5.0 |
| AMP | ✅ | ✅ |
| Early Stop | patience=5 | patience=10 |
| Stochastic Depth | — | ✅ 0.1 (drop_path) |
| Augmentation | RandomHFlip+Rot+ColorJitter+Affine+Erasing | 同 |

---

## 🔑 关键发现（Discussion 直接可用）

### 1. ConvNeXt +EMA 是最终最优模型
- 从初始 95.31% → 97.09%（+1.78%）
- wd=1e-3 + EMA 协同产生强正则化效果
- CNV 几乎不受影响（98.12% → 97.88%，-0.24%）
- DME +1.25%, DRUSEN +1.88%

### 2. Swin +EMA 经系统性优化后提升显著
- 从初始 95.06% → 96.19%（+1.13%）
- 增强（+0.81%）、Grid Search、stochastic depth 四项叠加
- EMA 拿 CNV -0.5% 换 DRUSEN +2.12% — 但仍净收益
- Swin 天花板 ≈ 96.2% — 受限于 28M 参数 + 注意力对微小病变的稀释效应

### 3. DRUSEN 是全局瓶颈
- ConvNeXt +EMA DRUSEN: 94.75% | Swin +EMA DRUSEN: 93.37%
- 特征：微小 RPE 隆起，无液体积聚，极易与 CNV 混淆
- 改进方向：高分辨率输入（384²）、多尺度特征融合（FPN）

### 4. Freeze 深度：小样本 ≠ 全量（方法学贡献）
- 2000 样本消融：freeze=2 最优（+0.86%）
- 25K 全量验证：freeze=0 胜出（-1.58% vs freeze=2）
- 消融结论不能线性外推 — 文献中少有人报告

### 5. Stochastic Depth 解决 Swin 过拟合
- drop_path=0.1 加开后方使 EMA 从拖累变为助推
- Swin EMA 从 Base 的 95.62% → 96.19%（+0.57%）
- 验证了原论文在微调场景下的必要性

### 6. CNN-Transformer 互补
- ConvNeXt EMA 错 93 例，Swin EMA 错 122 例，仅 75 例重叠
- Ensemble 理论可到 ~97.5% — 零额外训练成本

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

---

## ☑️ 待办

- [x] Grid Search 完成（20-epoch × 12 组 × 2 模型 = 480 epochs） ✅
- [x] ConvNeXt 最终训练（30-epoch, wd=1e-3, EMA） ✅ — 97.09%
- [x] Swin 最终训练（52-epoch, drop_path=0.1, EMA） ✅ — 96.19%
- [x] 测试评估（4 模型：Base/EMA × 2 架构） ✅
- [x] 可视化（训练曲线/混淆矩阵×2/ROC×2/Grad-CAM） ✅
- [x] Ablation（freeze depth, 8 组） ✅
- [x] 错误分析（Baseline + EMA 两套） ✅
- [x] final.ipynb 0 个 cell 报错，18/18 有输出 ✅
- [ ] 撰写 Word 报告（APU 格式：TNR 12pt, 1.5 倍行距）
- [ ] 提交：final.ipynb（含全部输出）+ Word 报告

---

## 📊 评分标准对照（总计 100分）

### Assignment 1 — 报告（40分）

| 评分项 | 满分 | 状态 | 要求 |
|---|---|---|---|
| **Introduction & Background** | 4 | 📝 待写 | OCT是什么、为什么需要自动分类、论文定位 |
| **Domain Knowledge** | 8 | 📝 待写 | 4种疾病临床特征+OCT图像特点+问题陈述+目标 |
| **Algorithm Justification** | 16 | 📝 待写 | 10–20篇文献综述+表格总结+ConvNeXt/Swin选择理由 |
| **Methods & References** | 12 | 📝 待写 | 方法论细节+数据集链接+APA格式参考文献 |
| **小计** | **40** | 📝 | |

### Assignment 2 — 代码 + Word文档（60分）

| 评分项 | 满分 | 状态 | 具体要求 | 对应位置 |
|---|---|---|---|---|
| **Model Implementation** | 24 | ✅ 22/24 | 数据预处理；两个不同架构DL模型的初始化、训练、评估；说明架构或训练方法的修改 | Cell 1–4：SHA256去重/增强/双模型/torchsummary/训练pipeline/CV2-GradCAM |
| **Tuning & Validation** | 18 | ✅ 18/18 | 超参调优并验证；最终模型构建与评估 | Cell 5,7–9,15：Grid Search 12组×20ep + 30–50ep最终训练 + 独立test集 |
| **Visualization & Critical Analysis** | 18 | ✅ 18/18 | 用合适工具可视化架构和性能；批判性分析模型表现 | Cell 8–13,16：曲线/混淆矩阵×2/ROC×2/torchinfo/Grad-CAM/Per-class/错误重叠 |
| **小计** | **60** | ✅ **58/60** | 报告还需补：代码注释、代码截图嵌入Word文档 | |
| **总计** | **100** | **58/100 已完成 + 42 待写** | | |
