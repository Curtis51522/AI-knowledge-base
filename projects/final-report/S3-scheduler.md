---
tags: [final-report, s3-scheduling]
created: 2026-07-13
---

# S3 CP-SAT Production Scheduler

## 功能

每日生产调度：给定 S2 需求预测 + 昨日余量，CP-SAT 算出每个面包产品的最优烘烤量。

## 输入

| 数据 | 来源 |
|------|------|
| 昨日余量 (Day-1 stock) | S1 YOLO / inventory |
| 需求预测 Q10/Q50/Q90 | S2 XGBoost quantile |
| 产品售价 | `bakery_sales_raw.csv` |
| 日产能 | 800 面包 |

## 输出

| 字段 | 说明 |
|------|------|
| `bake_plan` | 每个产品烘烤量 |
| `fresh_sold` / `day1_sold` | 鲜度分级销量 |
| `waste` / `shortage` | 浪费/缺货量 |
| `profit` / `revenue` | 预期利润/收入 |
| `materials` | 原材料需求估算 |
| `scenario_q10/q50/q90` | 三场景利润/浪费分析 |

## 数学公式

```
maximize  sum( price_i * fresh_sold_i + 0.5*price_i * day1_sold_i
              - 0.30*price_i * bake_i
              - 0.15*price_i * waste_i
              - 0.25*price_i * shortage_i )

s.t.      day1_sold_i <= day1_stock_i
          fresh_sold_i <= bake_i
          day1_sold_i + fresh_sold_i <= demand_i
          sum(bake_i) <= 800
          all vars >= 0, integer
```

## 使用方法

```bash
python s3_scheduling/scheduler.py                    # demo 6 products
python s3_scheduling/scheduler.py --full             # full 30-product
python s3_scheduling/scheduler.py --save plan.json   # save output
```

## 文件

- `s3_scheduling/scheduler.py` — 主调度器
- `s3_scheduling/outputs/` — 输出 JSON

## 与 S2 的对接

S2 分位数模型 → `load_s2_predictions()` → Q10/Q50/Q90 → `solve_scenarios()`

## 与 Dashboard 的对接

输出字段直接对应 [[dashboard-designs]] 的 Production Plan 面板：
- `bake_plan` → "建议烘烤量"
- `scenario_q10/q90` → "需求波动下的利润区间"
- `materials` → "原材料采购清单"

## 待做

- [ ] 7 天滚动计划 (`generate_7day_plan`)
- [ ] 对接真实 S2 模型输出
- [ ] 产品配方数据库（替换 DEFAULT_RECIPES）
- [ ] Dashboard API 端点
