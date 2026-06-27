---
tags: [final-report, s2-forecasting, references]
created: 2026-07-13
updated: 2026-07-13
---

# S2 预测模块 — 引用链 + 论文叙事逻辑

## 三实验叙事弧

```
实验 1: XGBoost 回归         实验 2: XGBoost 分类器        实验 3: XGBoost 分位数
   "日 SKU 回归天然不准"        "分类好一些但假警报多"         "校准完美，直接可用"
         ↓                           ↓                          ↓
    MAPE 57.3%                  Accuracy 71.8%              Coverage 81.7%
    比 lag_7_avg 仅 +3.7%        Precision 35.6%            Q10-Q90 宽度 5.83
    天气特征完全无用              ROC-AUC 66.1%              区间紧凑且校准精确
         ↓                           ↓                          ↓
    M5 (2022) 引用:             Bojer (2021) 引用:          Lim (2021) / Salinas (2020):
    "冠军方案也就这样"            "低销量 SKU 分类               "分位数回归 = 
                                 是务实选择"                  面向库存决策的预测"
         ↓                           ↓                          ↓
    论文 Method 章节              论文 Method 章节              论文 Method 章节
    (论证故事用)                  (论证故事用)                  + POS 前端输出
```

**核心逻辑**: 实验 1 和实验 2 只出现在论文 Method/Results 中，用于论证"为什么我们最终选择分位数回归"。实验 3 的分位数模型才是输出到 POS 前端供实际使用的。

---

## 核心引用

| 论文 | 期刊/会议 | 年份 | 引用理由 |
|------|-----------|------|----------|
| Makridakis et al., "M5 accuracy competition: Results, findings and conclusions" | *International Journal of Forecasting* | 2022 | M5 竞赛 30,490 SKU × 1,969 天。**结论：日 SKU 级别 MAPE 30-50% 是常态，分类 + 集成优于纯回归。** |
| Lim et al., "Temporal Fusion Transformer for Multi-horizon Time Series Forecasting" | *International Journal of Forecasting* | 2021 | 提出分位数回归做概率预测。输出 10%/50%/90% 分位数区间供库存决策。 |
| Salinas et al., "DeepAR: Probabilistic forecasting with autoregressive recurrent networks" | *International Journal of Forecasting* | 2020 | Amazon 出品，专门处理日粒度稀疏 SKU 的概率预测。 |

### 辅助引用

| 论文 | 期刊/会议 | 年份 | 引用理由 |
|------|-----------|------|----------|
| Bojer & Meldgaard, "Kaggle forecasting competitions: An overlooked learning opportunity" | *International Journal of Forecasting* | 2021 | 系统分析 XGBoost/LightGBM 在零售 SKU 分类上的表现。 |
| Koenker & Hallock, "Quantile Regression" | *Journal of Economic Perspectives* | 2001 | Pinball loss 理论基础。 |
| Chen & Guestrin, "XGBoost: A scalable tree boosting system" | *Proceedings of ACM SIGKDD* | 2016 | XGBoost 原始论文。 |

### 层级聚合（未来扩展）

| 论文 | 期刊 | 年份 | 引用理由 |
|------|------|------|----------|
| Hyndman et al., "Optimal Forecast Reconciliation" | *JASA* | 2016 | 单品不准 → 聚合到品类/周 → MAPE 显著降低。 |

---

## 三个实验的实际结果

### 实验 1: XGBoost 回归（对照组）
- 输入: 13 特征（product_id, 天气, 时间, 滞后）
- 输出: 日销量点预测
- **Test MAPE: 57.3%, R²: 0.758, RMSE: 2.78**
- 消融: no_lag → R²=-0.842, no_weather → R²=0.761（天气无用）
- 超参: max_depth=3, lr=0.1, n_estimators=100（432 组合 GridSearch）
- **功能: 论文论证用，不上 POS**

### 实验 2: XGBoost 分类器（对比组）
- 输入: 同上 13 特征
- 标签: `quantity > P70(product)` → 1 = 高需求日
- **Test Accuracy: 71.8%, F1: 38.5%, ROC-AUC: 66.1%**
- 超参: max_depth=3, lr=0.01, n_estimators=100（432 组合 GridSearch）
- **功能: 论文论证用，不上 POS**

### 实验 3: XGBoost 分位数回归（主推 → POS）
- 输入: 同上 13 特征
- 输出: Q10 / Q50 / Q90 三个分位数
- **Q10-Q90 Coverage: 81.7%（目标 80%）**
- **区间宽度: 5.83 单位（紧凑且校准精确）**
- 超参: max_depth=7, lr=0.1, n_estimators=200（Q50 调优，432 组合，Q10/Q90 继承）
- **功能: POS 前端输出 "donut 明天建议备 12 个（90% 把握）"**

---

## 论文黄金对比表

| 方法 | 指标 | 实际值 | 在论文中的角色 | POS 使用？ |
|------|------|--------|---------------|-----------|
| XGBoost 回归 | MAPE | 57.3% | 论证"天然不准" | 否 |
| XGBoost 分类器 | Accuracy | 71.8% | 论证"分类也不够好" | 否 |
| XGBoost 分位数 | Coverage | 81.7% | 最终推荐方案 | **是** |

---

## 论文故事线

1. 先做标准回归 → MAPE 57%，但消融揭示 lag_7_avg 主导（SHAP）、天气无用
2. 引用 M5 (2022): 日 SKU 回归天然高误差，Walmart 冠军也这样
3. 尝试分类 → Accuracy 71.8% 比回归好，但 Precision 仅 35.6%
4. 转向分位数回归 → Coverage 81.7%，校准完美
5. 结论: SKU 级预测应放弃精确回归和分类，采用分位数区间为库存决策服务

---

## 分位数 vs 概率 vs 回归

| | 输出 | 回答的问题 | POS 怎么用 |
|------|------|-----------|-----------|
| 分类器 | 概率 (0~1) | "明天要加备吗？" | 不给用户看 |
| 分位数 | 数量 (Q10/Q50/Q90) | "备多少个？" | **直接显示** |
| 回归 | 一个数 (5.3) | "卖几个？" | 不给用户看 |

---

## 待办

- [ ] 实验 4: 周层级聚合（Hyndman, 2016）— 未实现
- [ ] 分位数模型接入 POS Top-3 / 购物车推荐

---

## 更新 2026-07-13：代码冻结

所有模型代码不再修改。详见 [[S2-status]]。

剩余工作：
- [ ] 实验 4: 周层级聚合 (Hyndman, 2016)
- [ ] 统计检验: Diebold-Mariano test  
- [ ] 时间序列可视化
- [ ] 三模型对比表
- [ ] 2 个硬骨头产品 case study
- [ ] 分位数模型接入 POS
