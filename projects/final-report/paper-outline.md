# Paper Outline: S5 AI Brain — LLM-Mediated Multi-Objective Optimization

> Status: drafting | Target: IEEE Access / Applied Sciences | Updated: 2026-07-13

---

## 候选标题
1. **Safe LLM-Mediated Decision Making for Multi-Objective Production Optimization: A Bakery Operations Case Study**
2. **Pareto-Constrained LLM Selection for Small Business Operations Planning**
3. **Bridging MIP and LLMs: A Dominance-Filtered Decision Architecture for Bakery Production Scheduling**

首选 #1 — 明确点出 "safe" 和 "case study"，适合 IEEE Access 定位。

---

## Abstract 骨架

```
背景：Small retail businesses face multi-objective optimization (profit vs waste 
vs shortage) but lack access to sophisticated OR tools.

问题：Existing MIP solvers produce optimal plans but require expert interpretation; 
LLMs offer natural language interface but hallucinate recommendations without 
optimization guarantees.

方法：We propose a three-layer architecture — (1) MIP generates Pareto-optimal 
production plans, (2) a programmatic dominance filter eliminates strictly inferior 
candidates, (3) an LLM selects and explains the best plan with contextual constraints. 
The LLM is safety-constrained: it can only SELECT, never CREATE.

实验：Evaluated on a simulated bakery-cafe in Guangzhou, China with 30 bread products 
+ 15 drinks over N days. Compared against rule-based baselines and LLM-only approaches. 
Ablated each layer.

结果：S5 reduced waste by X%, improved profit by X%, with 100% constraint satisfaction 
(vs LLM-only at Y%). Owner satisfaction score: Z/5.

结论：Safe LLM-mediated optimization bridges the gap between mathematical rigor and 
operational accessibility for small businesses.
```

---

## 1. Introduction

### 1.1 Problem Background
- Small retail businesses face daily multi-objective decisions
- 30 bread products × 2 freshness levels × demand uncertainty × staffing constraints = NP-hard
- Existing tools: spreadsheets (error-prone), OR consultants (unaffordable)

### 1.2 Research Gap
- MIP solves optimization exactly → but output is numbers, not actionable advice
- LLMs give natural language advice → but hallucinate, ignore constraints, offer unreachable plans
- **No existing work combines MIP correctness with LLM accessibility under safety constraints**

### 1.3 Contributions (3点)
1. **Architecture**: Three-layer MIP→Dominance→LLM decision pipeline with provable safety (LLM can only SELECT from MIP-validated plans)
2. **Dominance Filter**: Pre-LLM elimination of strictly Pareto-dominated plans, reducing decision space and suppressing hallucination
3. **Validation**: N-day simulation on 45-product bakery in Guangzhou, quantitative comparison against 3 baselines

---

## 2. Related Work

### 2.1 Multi-Objective Optimization for Retail
- Perishable inventory: Nahmias (1982), Karaesmen et al. (2011)
- Bakery production: Van Donselaar et al. (2006), Ketzenberg et al. (2020)
- CP-SAT / MIP formulations for small retail

### 2.2 LLM-Augmented Optimization
- LLMCompiler (Kim et al., 2024) — DAG-based agent planning
- ReAct (Yao et al., 2023) — reasoning + acting
- Function calling for tool use (OpenAI, 2023)
- **Gap**: Existing work uses LLM for plan GENERATION; we use LLM for constrained plan SELECTION

### 2.3 Safe AI Decision Systems
- Human-in-the-loop (HITL) for verification
- Constitutional AI (Bai et al., 2022)
- **Gap**: No prior work enforces mathematical constraint satisfaction on LLM outputs in optimization contexts

---

## 3. Methodology (核心)

### 3.1 System Architecture

```
User Query (EN/CN)
     │
     ▼
DistilBERT Intent Classifier (8 intents)
     │
     ▼
6 Parallel Agents (Demand, Inventory, Production, Staffing, Promo, Profit)
     │
     ▼
┌─────────────────────────────────────────────────┐
│ LAYER 1: MIP Optimization                       │
│   maximize sum(rev_i - cost_i - waste_i -       │
│                stockout_i)                      │
│   s.t.   sum bake_i <= capacity                 │
│          flow_i + sales_i = demand_i            │
│          bake_i in Z+ (integer batch)           │
│   Output: 4 Pareto-optimal plans                │
│     A_aggressive / B_balanced /                 │
│     C_conservative / D_baseline                 │
├─────────────────────────────────────────────────┤
│ LAYER 2: Dominance Filter                       │
│   if profit_A > profit_B                        │
│   and waste_A <= waste_B                        │
│   and shortage_A <= shortage_B:                 │
│       eliminate B                               │
│   Output: true Pareto-optimal subset            │
├─────────────────────────────────────────────────┤
│ LAYER 3: LLM Decision Protocol                  │
│   Structured prompt with hierarchical rules     │
│   Rule: Dominance > Profit > Context            │
│   Output: PLAN=X|CONFLICT=Y/N|REASON=...        │
│   Safety: selected plan MUST exist in filtered  │
│           set (LLM can only SELECT)             │
└─────────────────────────────────────────────────┘
```

### 3.2 MIP Formulation

```
Indices: i in {1..30} products (+ 15 drinks handled separately)
Variables: b_i (bake), w_i (waste), s_i (shortage)
Parameters: d_i (demand from S2 quantile model), f_i (fresh stock), 
            day1_i, cap, price_i

Objective:
  max sum [price_i * min(b_i+f_i+day1_i, d_i) 
         - prod_cost * b_i 
         - waste_cost * w_i 
         - stockout_cost * s_i]

Constraints:
  sum b_i <= cap                          (capacity)
  b_i + f_i + day1_i + s_i = d_i + w_i   (flow balance)
  b_i >= 0, integer                       (batch constraint)

Pareto frontier: 4 risk-preference points alpha in {0, 0.25, 0.5, 1.0}
  d_i(alpha) = d_low + alpha * (d_high - d_low)
  where d_low = S2 Q10, d_high = S2 Q90
```

### 3.3 Dominance Filter Algorithm
```
def dominance_filter(plans):
    dominated = set()
    for each (A, B) in plans:
        if profit_A > profit_B 
        and waste_A <= waste_B 
        and shortage_A <= shortage_B:
            dominated.add(B)
    return plans \ dominated
```
**Theorem**: Filtered plans are the true Pareto-optimal subset among candidates.

### 3.4 LLM Decision Protocol
- Structured prompt with hierarchical rules
- Rule priority: Dominance > Profit-first > Context adjustment
- Output format: `PLAN=X|CONFLICT_ADDRESSED=Y/N|REASON=...`
- Validation: selected plan must exist in filtered set → safety guarantee

---

## 4. Experimental Design

### 4.1 Deployment Context
- Simulated bakery-cafe in Guangzhou, China
- 30 bakery products + 15 drinks
- Sales data: 3-year synthetic dataset (2021-2023) based on French Bakery distribution
- Daily capacity ~720 units (breads)
- S2 quantile model provides demand intervals (Q10/Q50/Q90) as MIP input

### 4.2 Baselines
| 方案 | MIP | Dominance | LLM | 说明 |
|------|-----|-----------|-----|------|
| **S5-Full** | ✅ | ✅ | ✅ | 完整系统 |
| **S5-NoDominance** | ✅ | ❌ | ✅ | LLM从原方案选择（无安全过滤）|
| **S5-RuleBased** | ✅ | ✅ | ❌ | 总是选 B_balanced |
| **LLM-Only** | ❌ | ❌ | ✅ | 纯 LLM 建议（无 MIP 约束）|

### 4.3 Metrics
| 指标 | 定义 | 来源 |
|------|------|------|
| Constraint Satisfaction Rate | 决策不违反产能/库存上限的比例 | 自动计算 |
| Waste Reduction % | (实际浪费 - 基线浪费) / 基线浪费 | S1 inventory |
| Profit Improvement % | (实际利润 - 基线利润) / 基线利润 | S4 sales |
| Decision Latency (ms) | 端到端响应时间 | S5 elapsed_ms |
| Owner Trust Score | 1-5 Likert 主观评分 | 问卷 |

### 4.4 Ablation Study
1. Remove Dominance Filter → LLM sees 4 plans instead of filtered set
2. Remove Cross-Agent Data → agents run independently without re-run
3. Remove LLM Decision → always select B_balanced
4. Vary demand uncertainty alpha → sensitivity analysis across S2 quantile intervals

---

## 5. Expected Results (占位符 — 实测后填入)

| 方案 | 浪费(日均) | 短缺 | 利润(日均) | 约束满足率 | 延迟 |
|------|-----------|------|-----------|-----------|------|
| S5-Full | ? | ? | ? | 100% | ~5s |
| S5-NoDominance | ? | ? | ? | 100% | ~5s |
| S5-RuleBased | ? | ? | ? | 100% | ~2s |
| LLM-Only | ? | ? | ? | <80%? | ~3s |

---

## 6. Discussion Points

1. Why constraint satisfaction matters for small business — one wrong recommendation = real money lost
2. Dominance filter as "free safety" — eliminates bad plans before LLM sees them
3. Generalizability — architecture applies to any perishable-inventory small retail
4. Limitations: single-bakery simulation, synthetic sales data, 45-product scale

---

## 7. 目标期刊

| 优先级 | 期刊 | IF | 中科院 | 审稿周期 | APC |
|--------|------|-----|--------|----------|-----|
| 🥇 | IEEE Access | 3.4 | Q2 | 4-8周 | $1,950 |
| 🥈 | Applied Sciences (MDPI) | 2.5 | Q3-Q4 | 3-5周 | CHF 1,800 |
| 🥉 | PLOS ONE | 3.7 | Q2-Q3 | 4-8周 | $2,165 |
| 备选 | Electronics (MDPI) | 2.6 | Q3-Q4 | 3-5周 | CHF 1,800 |
| 备选 | PeerJ Computer Science | 2.5 | Q3-Q4 | 4-6周 | $1,395 |

---

## 8. 待办清单

### Phase 1: 数据收集
- [ ] 运行完整 S1-S5 pipeline 收集决策日志
- [ ] 每天导出 sales / waste / profit 数据
- [ ] 收集团队反馈（1-5分 + 自由评论）

### Phase 2: 实验
- [ ] 跑 4 组 baseline 对比（用收集到的需求数据回放）
- [ ] 消融实验 4 组
- [ ] 绘制对比图表

### Phase 3: 写作（2-3周）
- [ ] Methodology 章节（已有代码，直接翻译+形式化）
- [ ] Related Work 文献检索 15-20 篇
- [ ] Introduction + Abstract
- [ ] Results + Discussion
- [ ] 格式化（IEEE Access 模板）

---

## 9. S2 与 S5 的关系

S2（预测模块）输出分位数需求区间 → S5（LLM 决策模块）作为 MIP 的需求参数。

```
S2 分位数模型                 S5 MIP 优化
─────────────                ──────────
Q10 d_low  ──────────────→  d_i(alpha=0)    = baseline 需求
Q50        ──────────────→  d_i(alpha=0.25) = 保守需求
Q90 d_high ──────────────→  d_i(alpha=1.0)  = 激进需求
```

两篇论文的关系：
- **Paper A (S1+S2)**: 视觉识别 + 销售预测 → 投计算机视觉/预测类期刊
- **Paper B (S3+S5)**: MIP 调度 + LLM 决策 → 投 AI/OR 交叉期刊（本文档）
