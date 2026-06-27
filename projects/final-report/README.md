# Bakery AI System - Final Report

## Project Goal
Design and implement a multi-agent AI operations system for a medium-sized bakery-cafe in Kuala Lumpur, Malaysia. The system integrates computer vision, demand forecasting, shift scheduling, POS checkout (with combo recommendations), and a multi-agent AI Brain for real-time decision support.

**Scale:** 6 bakery products, 6 coffee drinks, 10 employees, 2 ovens, 2 checkout counters (main bakery counter + secondary coffee counter, barista doubles as cashier). Rest day: Monday.

---

## Current Stage: Demo-Ready + Pre-Field Test
System fully built, S5 code-reviewed and hardened. Paper outline written. **Demo at bakery: June 25 (tomorrow).**

---

## Progress (Completed)

### S1 - Visual Recognition (YOLO)
- **待升级**: YOLOv8n → **YOLO11s**（更好的注意力机制，区分相似面包更准）
- **待扩展**: 6 类 → 更多品类（需找新的烘焙数据集）
- Checkout with FIFO inventory deduction
- Fresh Batch Inflow for new production scanning
- HITL (Human-in-the-Loop) correction log

### S2 - Demand Forecasting (XGBoost)
- Per-product XGBoost quantile regression models (6 products)
- 7-day forecast with low/mid/high confidence intervals
- Weather data integration via VisualCrossing API
- Auto-refresh every 30 minutes

### S3 - Shift Scheduling (OR-Tools CP-SAT)
- OR-Tools CP-SAT solver, demand-driven auto-staffing
- Dual-role support, sick leave auto-replacement, shift swaps
- Past-date locking + KPI snapshot persistence
- Employee coverage statistics & fairness metrics
- **待实现: 员工签到系统 (PIN码打卡)** → 归入 S3 Dashboard 模块，不做在 POS 上

### S4 - POS Frontend + Combo Engine (BFF Architecture)
- Responsive Web POS, JWT auth (Staff/Manager roles)
- Five-dimensional combo scoring, Day-1 dynamic discount
- Post-checkout FIFO deduction + receipt, LLM sales script
- EN/BM bilingual support throughout all UI
- Smart Top-3 bundle recommendations
- AI-generated sales script for cashiers
- **S4 已完成优化 (2026-06-25):**
  - ✕ 一键删除购物车行
  - − / + 一键调整数量
  - ⚙ Edit 改为齿轮图标，Error Type 已删除
  - 💳 支付弹窗 (Cash/Card/QR + 找零)
  - 🧾 小票显示 + 打印
  - 🔄 S5 折扣加载后自动重绘 POS
  - 🟢 产品卡片固定 20%/Top-3 走 S5 折扣路径分离
  - 🟡 Fresh/Day-1 分开显示 + 购物车按鲜度区分
  - ⌨️ ESC 键关弹窗
  - 🗑️ Clear Cart 按钮

### S5 - AI Brain (Multi-Agent Engine) 🔧 2026-06-24
- DistilBERT intent classifier (8 intents), 6 programmatic agents
- MIP Pareto plan generation + LLM plan selection & synthesis
- System alerts: background monitoring every 5 minutes (inventory, forecast, schedule, trends)
- Supports English, Bahasa Malaysia, and mixed EN-BM input

#### S5 Deep Review + Hardening (2026-06-24)
- **Code review**: full call chain traced (/query → parse → classify → agents → arbitrate → synthesize)
- **3 critical bugs fixed**:
  | Bug | File | Fix |
  |-----|------|-----|
  | Arbitrator defaulted baker=1 when staffing API failed | `arbitrator.py:239` | Default→0 + confidence gate |
  | LLM Planner's date field silently ignored | `server.py:428-430` | Now captured into params |
  | LLM Planner's product name not validated | `server.py:431-439` | Normalize + fallback to local extraction |
- **Intent classifier overhaul**: 85% → **98% accuracy** (54 benchmarks)
  - Keyword list: removed overly-generic words, added Malay profit/ranking/comparison terms
  - Cross-validation layer: DistilBERT + keyword disagreement detection with 3 trigger rules
  - Profit-force rule: Malay "untung/rugi/keuntungan" auto-boost profit_analysis
- **Pre-flight checks passed**: Python 3.13, 10/10 deps, MySQL (7 inventory + 1045 txn), YOLO 50MB, XGBoost 6 models, DistilBERT 256MB

### Recent UI/UX Improvements (2026-06-11)
- Full EN/BM language toggle with ~120 translation keys
- Freshness switched to midnight-based (was 24-hour)
- Dynamic discounts with 20% floor
- Cart-only combo pairing logic
- Savings-based Top-3 sorting for coffee-only scenarios
- Fixed showPanel race condition (await redirect bug)
- Fixed ? to checkmark character in Plan Options
- Removed all Day-2/Near-Expired residual code (only Fresh/Day-1 remain)
- Demo script written for merchant presentation

---

## Known Limitations (Before Field Test)

| # | Issue | Impact |
|---|-------|--------|
| 1 | **No real sales data** | All models trained on synthetic seed data; forecast accuracy unverified |
| 2 | **YOLO not tested with real camera** | Only tested with static images; real lighting, angles, occlusion unknown |
| 3 | **Revenue = RM0** | Profit agent always shows negative margin until real transactions are recorded |
| 4 | **Two servers require manual start** | S5 (:8001) and main server (:8002) must be started separately |
| 5 | **MILP occasionally infeasible** | Graceful fallback to LP + rounding; plan is feasible but not optimal |
| 6 | **Not integrated with oven/kitchen** | Oven scheduling not yet connected to real equipment |

---

## Next Steps

### Publication 📄
- [x] Paper outline: [[paper-outline|LLM-MIP Decision Architecture]] — targeting IEEE Access / Applied Sciences (Q2-Q3)
- [ ] Collect real bakery data for experimental section (Phase 1: starting tomorrow)
- [ ] Run 4 baseline comparisons + ablation study (Phase 2: post field test)
- [ ] Write Methodology, Related Work, Results (Phase 3)

### Field Test (Tomorrow — June 25)
- [x] Prepare laptop/deployment environment
- [x] S5 code hardened + intent classifier 98%
- [x] Both servers verified running (:8001 + :8002)
- [ ] Seed database with realistic initial inventory data
- [ ] Bring USB camera and test YOLO at checkout counter
- [ ] Follow [[../DEMO_SCRIPT.md|DEMO_SCRIPT]]: login → POS → Top-3 → forecast → schedule → inventory → AI Brain → alerts

### During Field Test (1-2 weeks)
- [ ] Collect real sales data daily
- [ ] Log all S5 AI Brain decisions + owner reactions
- [ ] Test YOLO accuracy under real lighting and tray conditions
- [ ] Gather staff feedback on POS usability
- [ ] Gather owner feedback on AI Brain recommendations
- [ ] Log all bugs and UX friction points

### Post Field Test
- [ ] Retrain XGBoost models on real sales data
- [ ] Fine-tune YOLO with real bakery images if needed
- [ ] Retrain DistilBERT intent classifier with real queries
- [ ] Adjust S3 constraint model based on actual staffing needs
- [ ] Iterate combo scoring weights based on owner preferences
- [ ] Write paper experimental section with real data
- [ ] Finalize documentation for final report submission
