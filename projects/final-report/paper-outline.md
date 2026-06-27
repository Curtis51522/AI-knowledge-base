# Paper Outline: Integrated AI System for Small Bakery Operations

> Status: drafting | Target: IEEE Access / Applied Sciences | Updated: 2026-07-13

---

## 候选标题
1. **Integrated Computer Vision and Probabilistic Forecasting for Bakery Production Optimization: A Pipeline Approach**
2. **From Shelves to Schedule: A Multi-Module AI System for Small Bakery Operations**
3. **YOLO-Driven Inventory and Quantile-Guided Scheduling for Perishable Retail**

首选 #2 — 点出"multi-module"和"small bakery"，适合应用类期刊。

---

## Abstract 骨架

```
背景：Small bakeries face daily decisions — what to bake, how many, based on
yesterday's leftovers and uncertain demand. Most rely on owner intuition.

问题：Existing solutions are fragmented — computer vision for inventory, 
ML for forecasting, OR for scheduling — but no integrated pipeline exists
that connects visual stock monitoring to production planning.

方法：We propose a three-module architecture — (1) YOLO-based visual inventory 
recognition (30 product categories), (2) XGBoost quantile regression for 
demand forecasting with prediction intervals, (3) CP-SAT optimization for 
production scheduling that maximizes profit under capacity constraints.
Output is unified in a real-time operations dashboard.

实验：Evaluated on a simulated Guangzhou bakery-cafe (30 breads + 15 drinks) 
over 3 years of sales data. Includes employee KPI system with BSC+Z-Score normalization for multi-role performance comparison. Compared against naive baseline, rule-based 
scheduling, and individual module ablations.

结果：Quantile demand coverage 80.3%, scheduling reduces waste by X%, 
improves profit by X% vs baseline. Dashboard enables single-glance 
operational decisions.

结论：An integrated visual-to-production pipeline is feasible and 
beneficial for small perishable-goods retailers without dedicated 
operations teams.
```

---

## 1. Introduction

### 1.1 Problem Background
- Small bakeries make daily multi-objective decisions under uncertainty
- 30 bread products × freshness tiers (Fresh/Day-1) × demand volatility
- Existing tools: spreadsheets (error-prone), owner intuition (biased)
- Computer vision + ML + OR exist separately but no integrated pipeline

### 1.2 Research Gap
- YOLO for retail inventory exists → but not connected to production planning
- ML demand forecasting exists → but point predictions are unreliable at SKU level
- OR scheduling exists → but requires manual demand input
- **No end-to-end system: visual inventory → probabilistic forecast → optimal schedule**

### 1.3 Contributions (3点)
1. **Integrated pipeline**: YOLO recognition → XGBoost quantile forecasting → CP-SAT scheduling, connected in a single data flow
2. **Quantile demand forecasting**: replaces unreliable point predictions with calibrated Q10/Q50/Q90 intervals for inventory decisions
3. **Multi-role KPI system**: BSC + Z-Score normalization + AHP for fair cross-role performance comparison (baker, barista, cashier, manager) in a small food-service team
4. **Real-world simulation**: 3-year, 45-product Guangzhou bakery case study with dashboard deployment

---

## 2. Related Work

### 2.1 Computer Vision for Retail Inventory
- YOLOv8/v11 for shelf monitoring (Redmon et al., 2018)
- Fine-grained food classification (Bossard et al., 2014 — Food-101)
- Roboflow-annotated bakery datasets
- **Gap**: CV systems stop at recognition; no integration with operational decisions

### 2.2 Demand Forecasting for Perishable Goods
- M5 Competition: daily SKU-level, LightGBM dominates (Makridakis et al., 2022)
- Quantile regression for probabilistic forecasting (Koenker & Hallock, 2001)
- Temporal Fusion Transformer (Lim et al., 2021)
- **Gap**: Forecasting research targets accuracy metrics; practitioners need decision intervals

### 2.3 Production Scheduling
- Perishable inventory optimization (Nahmias, 1982)
- CP-SAT for small-batch production (Google OR-Tools)
- Multi-objective production planning (Ketzenberg et al., 2020)
- **Gap**: Schedulers assume demand is known; real demand is uncertain

---

## 3. Methodology (核心)

### 3.1 System Architecture

```
Raw Image (camera)           Historical Sales Data
      │                              │
      ▼                              ▼
┌──────────┐              ┌────────────────────┐
│ S1: YOLO │              │ S2: XGBoost         │
│ 30-class │              │ Quantile Regression │
│ bakery   │              │ Q10 / Q50 / Q90    │
│ detector │              └────────┬───────────┘
└────┬─────┘                       │
     │                             │ demand intervals
     │ Day-1 stock                 │
     ▼                             ▼
┌──────────────────────────────────────────┐
│           S3: CP-SAT Scheduler            │
│  maximize: profit - waste - shortage      │
│  s.t.: capacity, freshness, demand bounds │
│  output: daily production plan            │
└────────────────────┬─────────────────────┘
                     │
                     ▼
┌──────────────────────────────────────────┐
│              Dashboard                     │
│  - Current stock (from S1)                │
│  - Demand forecast (from S2)              │
│  - Production plan (from S3)              │
│  - Expected profit / waste / shortage     │
└──────────────────────────────────────────┘
```

### 3.2 S1: YOLO Visual Inventory Recognition
- 30 bakery product classes
- Dataset: merged Roboflow annotations, 18,243 train / 2,206 val / 2,205 test
- YOLOv11 with best params from grid search
- Output: daily stock counts (Fresh, Day-1)

### 3.3 S2: XGBoost Quantile Demand Forecasting
- 13 features: product_id, weather (5), time (4), lag (3)
- Three independent XGBoost quantile regressors: Q10, Q50, Q90
- Pinball loss: rho_alpha(u) = alpha*max(u,0) + (1-alpha)*max(-u,0)
- Hyperparameter tuning: 432-combination GridSearchCV (5-fold) per model
- Train 2021-2022, val 2023H1, test 2023H2
- Output: prediction intervals for each product

### 3.4 S3: CP-SAT Production Scheduling
- Decision variables: bake_quantity_i for each product i
- Objective: maximize sum(price_i * sold_i - cost_i * bake_i - waste_cost_i * waste_i - stockout_cost_i * shortage_i)
- Constraints: total bake <= capacity, flow balance, freshness tiers
- Demand from S2: d_low = Q10, d_high = Q90
- Output: daily production plan per product

### 3.5 Employee KPI System
- BSC (Balanced Scorecard) framework: Financial / Customer / Internal Process / Learning & Growth
- Z-Score normalization to eliminate inter-role differences (baker vs barista vs cashier)
- 3-step fairness pipeline: within-role Z-Score ? BSC weighted aggregation ? cross-role unified ranking
- POS auto-collection: 5-7 KPIs per role, monthly trend dashboard, quarterly formal review
- AHP (Analytic Hierarchy Process) for scientific weight determination (CR<0.1)

> Research: [[kpi-research]] | [[employee-KPI-normalization-research]]

### 3.6 Dashboard (4 screens)
### 3.5 Dashboard (4 screens)

#### Landing Screen
- Key metrics at a glance: today demand, current stock, staff on duty, yesterday revenue
- Top alerts: low stock, staffing gaps, anomalies
- Drill-down shortcuts to 4 sub-dashboards

#### Demand Forecasting Dashboard (3 panels)
1. **Demand Forecast**: S2 7-day per-product forecast grid with trend arrows
2. **Production Plan**: S3 bake recommendations (demand x 1.05 buffer) + 7-day view
3. **Raw Material Procurement**: weekly requirement x recipes x (1+waste%) - current stock, with urgency classification (urgent / order / sufficient)

#### Inventory Dashboard (3 panels)
1. **Bread Stock**: batch_inventory by Fresh/Day-1/Total, sufficiency status
2. **Baking Materials**: raw_materials, auto-deduct from batch scans
3. **Coffee Materials**: raw_materials filtered by category, auto-deduct from POS

#### Revenue Dashboard (5 panels)
1. **Key Numbers**: today revenue / profit / order count / avg ticket
2. **Payment Breakdown**: Cash / Card / QR split + Bread vs Coffee category share
3. **Sales Ranking**: product x quantity x amount x profit, same-day filter
4. **Profit Trend**: 7-day trend, bread vs coffee split
5. **Historical Query**: date range + granularity (day/week/month) x product

#### Shift+KPI Dashboard (3 panels)
1. **Today Attendance**: real-time punch-card status
2. **Weekly Shift**: 7-day grid
3. **Monthly KPI**: attendance rate / punctuality / goal achievement / team rate x Z-score ranking

> Full design: [[dashboard-design]] | [[dashboard-designs]]

---

## 4. Experimental Design

### 4.1 Deployment Context
- Simulated bakery-cafe, Guangzhou, China
- 30 bakery products + 15 drinks
- 3-year dataset (2021-2023), ticket-level
- Daily capacity: 800 breads + 300 drinks
- Real Guangzhou weather (Open-Meteo) + Chinese holidays

### 4.2 S2 Experiments (Demand Forecasting)
| 实验 | 模型 | 指标 | 结果 |
|------|------|------|------|
| Baseline | lag_7_avg naive | MAPE | ~55% |
| Regression | XGBoost regressor | MAPE | 35.3% |
| Classifier | XGBoost classifier | Acc/F1 | 67.2%/53.2% |
| **Quantile** | **XGBoost Q10/Q50/Q90** | **Coverage** | **80.3%** |

### 4.3 S3 Experiments (Scheduling)
| 方案 | 说明 | 预期 |
|------|------|------|
| Naive | Always bake mean demand | 高浪费 |
| Rule-based | Demand × 1.1, round up | 中等 |
| **CP-SAT** | **Optimization with S2 intervals** | **最优** |

### 4.4 Metrics
| 指标 | 定义 |
|------|------|
| Waste rate | units wasted / units baked |
| Stockout rate | demand gaps / total demand |
| Profit margin | (revenue - cost - waste) / revenue |
| Forecast coverage | fraction of demand in [Q10, Q90] |

---

## 5. Expected Results (占位符)

| 模块 | 核心指标 | 值 |
|------|----------|-----|
| S1 YOLO | mAP50 | ? |
| S2 Quantile | Q10-Q90 Coverage | 80.3% |
| S3 CP-SAT | Waste reduction vs baseline | ? |
| Dashboard | Owner usability score | ? |

---

## 6. Discussion Points

1. Why quantile regression beats point prediction for operational decisions
2. The value of prediction intervals (Q10-Q90) vs single numbers in scheduling
3. Integration challenges: connecting CV output to ML input to OR constraints
4. Generalizability to other perishable retail (convenience stores, florists)
5. Limitations: synthetic drink data, simulated deployment, single-location

---

## 7. 目标期刊

| 优先级 | 期刊 | 理由 |
|--------|------|------|
| 🥇 | IEEE Access | 综合性，接受应用系统论文 |
| 🥈 | Applied Sciences (MDPI) | 快，接受 case study |
| 🥉 | Expert Systems with Applications | 更匹配但审稿慢 |

---

## 8. 待办

### S1
- [ ] YOLOv11 训练 30 类

### S2
- [ ] 实验 4: 周层级聚合
- [ ] 统计检验 + 可视化

### S3
- [ ] CP-SAT 调度器实现

### 前端
- [ ] Dashboard 改造

### 论文
- [ ] Introduction + Related Work 写作
- [ ] Methodology 写作
- [ ] Results 填入实测数据
