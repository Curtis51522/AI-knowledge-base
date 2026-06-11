# DL Project: OCT Retinal Image Classification — ConvNeXt vs Swin-Tiny

## 项目目标
- 使用两个 SOTA 深度学习模型（ConvNeXt-Base 87.5M / Swin-Tiny 27.5M）对 OCT 视网膜图像进行四分类（CNV / DME / DRUSEN / NORMAL）
- 基于 OCT2017 数据集（Kermany et al., 2018）构建清洗后的子集 OCT2017_30K_V2
- 完成完整的 DL 作业流程：超参调优 → 模型训练 → 测试评估 → 消融实验 → 论文撰写

## 当前进展（实验已全部完成 ✅）

### 数据集
- SHA256 全局去重 → 分层划分，移除 237 张跨类重复 + 7,324 张类内重复
- Train: 24,972 张（自然分布），Test: 3,198 张（每类 800 张平衡）
- **Train/Test 零重叠**（SHA256 验证通过）

### 模型结果

| 指标 | ConvNeXt-Base | Swin-Tiny |
|------|--------------|-----------|
| 参数量 | 87.5M | 27.5M |
| 最佳验证准确率 | 0.9701（epoch 13） | 0.9690（epoch 29） |
| 测试准确率 | 0.9531 | **0.9562** |
| Precision | 0.9541 | **0.9572** |
| Recall | 0.9531 | **0.9562** |
| F1-Score | 0.9530 | **0.9562** |
| AUC | 0.9964 | 0.9964 |
| 推理速度 | 5.86 ms/img | **5.21 ms/img** |

### 已完成模块
- [x] Grid Search（3 lr × 2 bs = 6 组合 × 2 模型，seed=99）
- [x] 正式训练（CosineAnnealingLR + AdamW + AMP + EarlyStopping patience=5）
- [x] 测试评估（accuracy / precision / recall / F1 / AUC / 混淆矩阵 / ROC）
- [x] 类权重（balanced） + EMA（0.9999）
- [x] Swin-Tiny 专用优化：warmup=3 epochs + grad_clip_norm=5.0
- [x] 消融实验（freeze depth 分析）
- [x] 错误分析（Both correct 93.8%, Both wrong 2.8%）
- [x] 推理速度对比
- [x] 所有结果保存至 `notebook/outputs/`（.pth / .json / .png）

## 当前卡点
- **无技术卡点**，所有实验已跑完
- ConvNeXt 存在轻微过拟合（val_loss 在后期震荡，train_loss 持续下降），Swin-Tiny 表现更稳定
- 下一阶段为论文写作，需将实验结果嵌入学术论文

## 下一步要做什么
1. **撰写论文**（Word，APU 论文格式：Times New Roman 12pt，1.5 倍行距）
2. 论文结构：
   - Introduction
   - Literature Review（15–20 篇文献，主要为 2021–2025）
   - Methodology（数据集 SHA256 去重流程 + 模型定义 + 训练协议）
   - Results（网格搜索结果 / 训练曲线 / 测试指标 / 混淆矩阵 / ROC / 推理速度 / 消融实验 / 错误分析）
   - Discussion（val-test gap / Swin 效率优势 / 类权重影响 / DRUSEN 泛化 / 未做 patient-level split 的局限性）
   - Conclusion
3. 将 `outputs/` 中的图表嵌入论文
4. 提交代码（`final.ipynb`）+ 论文

## 备注
- 代码位置：`C:\Users\Curtis\Desktop\learningmaterials\SEMESTER3\DL\notebook\final.ipynb`
- 数据集构建脚本：`scripts\build_dataset.py`
- 所有代码无中文，使用动态路径
- 作业红线：禁止用 "ANN + dense layers on CSV" 结构，已严格遵守
