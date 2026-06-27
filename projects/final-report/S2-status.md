---
tags: [final-report, s2-forecasting, status]
created: 2026-07-13
---

# S2 状态：代码冻结

## 决策

**三个模型代码已冻结，不再修改。** 剩余工作全部是论文补充实验和图表，不涉及模型变更。

## 三个模型最终结果

| # | 模型 | 核心指标 | 超参 | GridSearch | POS？ |
|---|------|----------|------|:---:|:---:|
| 1 | XGBoost Regression | Test MAPE 57.3%, R² 0.758 | max_depth=3, lr=0.1, n=100 | 432 combos | 否 — 论文对照组 |
| 2 | XGBoost Classifier | Test Acc 71.8%, F1 38.5%, ROC-AUC 66.1% | max_depth=3, lr=0.01, n=100 | 432 combos | 否 — 论文对比组 |
| 3 | XGBoost Quantile | Q10-Q90 Coverage 81.7%, Width 5.83 | max_depth=7, lr=0.1, n=200 | 432 combos | **是 — 唯一上线** |

### 实验 3（分位数）详细指标

| 指标 | 值 | 目标 | 偏差 |
|------|-----|------|------|
| Q10-Q90 Coverage | 81.7% | 80% | +1.7% |
| Q10-Q50 Coverage | 43.7% | 40% | +3.7% |
| Q50-Q90 Coverage | 38.0% | 40% | -2.0% |
| 80% Interval Width | 5.83 | — | — |
| 50% Interval Width | 2.56 | — | — |
| ≥80% coverage 产品数 | 28/45 | — | — |
| <75% coverage 产品数 | 5/45 | — | — |

### 实验 1（回归）关键发现

- Test MAPE (57.3%) **好于** Train MAPE (61.2%) — 模型泛化强，不过拟合
- 比 baseline (lag_7_avg) R² 仅提升 5.2% (0.721→0.758)
- 天气特征完全无用: no_weather R²=0.761 > 完整 R²=0.758
- Lag 特征是一切: no_lag R²=-0.842
- 4/45 产品 MAPE < 30%，9/45 产品 MAPE < 50%

### 跨模型一致性

- 2 个产品（12, 22）三个模型都差 → 数据本身有问题
- 11 个产品三个模型都稳 → "可预测 SKU"
- 分位数覆盖与区间宽度 r=-0.835：高销量产品区间宽但覆盖反而低，暗示结构性波动

---

## 论文叙事弧

```
实验 1: 回归     →  "日 SKU 点预测不可行"     (M5 2022)
实验 2: 分类器   →  "分类有进步但假警报多"    (Bojer 2021)  
实验 3: 分位数   →  "区间预测校准完美"        (Lim 2021, Salinas 2020)
实验 4: 周聚合   →  "聚合后 MAPE 骤降"        (Hyndman 2016)
```

实验 1-2 为论文故事服务，实验 3 输出到 POS，实验 4 做稳健性检验。

---

## 剩余工作（全是论文补充，不碰模型代码）

### 必须做

- [ ] **实验 4: 周层级聚合** — 日 SKU → 周品类 groupby，对比聚合前后 MAPE
- [ ] **统计检验** — Diebold-Mariano test 证明分位数显著优于回归
- [ ] **时间序列可视化** — 3-5 个代表产品的预测 vs 实际图
- [ ] **三模型对比表** — 论文 Results 章节的黄金表格

### 加分项

- [ ] 2 个硬骨头产品（12, 22）的 case study
- [ ] 分位数模型 API 端点
- [ ] 接入 POS Top-3 / 购物车推荐

### 写论文时补（不改代码）

- [ ] 消融实验结论文字
- [ ] SHAP 分析文字（天气无用 = 可发表的负面结果）
- [ ] Discussion: 为什么分位数优于回归/分类
- [ ] 引用链完善（BibTeX 格式）

---

## 文件清单

| 文件 | 状态 |
|------|:--:|
| `s2_forecasting/train_xgboost.py` | ✅ 冻结 |
| `s2_forecasting/train_classifier.py` | ✅ 冻结 |
| `s2_forecasting/train_quantile.py` | ✅ 冻结 |
| `s2_forecasting/outputs/xgboost_model.pkl` | ✅ |
| `s2_forecasting/outputs/classifier_model.pkl` | ✅ |
| `s2_forecasting/outputs/quantile_model_q10.pkl` | ✅ |
| `s2_forecasting/outputs/quantile_model_q50.pkl` | ✅ |
| `s2_forecasting/outputs/quantile_model_q90.pkl` | ✅ |
| `s2_forecasting/outputs/metrics.json` | ✅ |
| `s2_forecasting/outputs/classifier_metrics.json` | ✅ |
| `s2_forecasting/outputs/quantile_metrics.json` | ✅ |
| `s2_forecasting/outputs/per_product_metrics.csv` | ✅ |
| `s2_forecasting/outputs/classifier_per_product.csv` | ✅ |
| `s2_forecasting/outputs/quantile_per_product.csv` | ✅ |

---

## 编码规则（备忘）

1. 每个模型必须独立 GridSearchCV，禁止从其他模型继承超参
2. 分位数 Q10/Q90 可继承 Q50 结构参数（唯一例外，已在 docstring 注明理由）
3. 所有参数组合数 ≥ 432
4. CV = 5 folds, random_state = 42

---

## 下一步

实验 4（周层级聚合）→ 统计检验 → 可视化 → 论文写作
