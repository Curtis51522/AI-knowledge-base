# Bakery AI System - Final Report

## Project Goal
Design and implement a multi-agent AI operations system for a medium-sized bakery-cafe in Kuala Lumpur, Malaysia. The system integrates computer vision, demand forecasting, shift scheduling, POS checkout (with combo recommendations), and a multi-agent AI Brain for real-time decision support.

**Scale:** 6 bakery products, 6 coffee drinks, 10 employees, 2 ovens, 2 checkout counters (main bakery counter + secondary coffee counter, barista doubles as cashier). Rest day: Monday.

---

## Current Stage: Pre-Deployment Polish & Demo Preparation
System is fully built and running locally. Next step: bring to the bakery for real-environment testing, collect owner and staff feedback, iterate based on actual operational needs.

---

## Progress (Completed)

### S1 - Visual Recognition (YOLO)
- YOLOv8n trained, supports 6 product detection
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

### S4 - POS Frontend + Combo Engine (BFF Architecture)
- Responsive Web POS, JWT auth (Staff/Manager roles)
- Five-dimensional combo scoring, Day-1 dynamic discount
- Post-checkout FIFO deduction + receipt, LLM sales script
- EN/BM bilingual support throughout all UI
- Smart Top-3 bundle recommendations
- AI-generated sales script for cashiers

### S5 - AI Brain (Multi-Agent Engine)
- DistilBERT intent classifier (8 intents), 6 programmatic agents
- MIP Pareto plan generation + LLM plan selection & synthesis
- System alerts: background monitoring every 5 minutes (inventory, forecast, schedule, trends)
- Supports English, Bahasa Malaysia, and mixed EN-BM input

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

### Publication
- [ ] Paper outline: [[paper-outline|LLM-MIP Decision Architecture]] — targeting IEEE Access / Applied Sciences (Q2-Q3)

### Field Test Preparation
- [ ] Prepare laptop/deployment environment for on-site testing
- [ ] Seed database with realistic initial inventory data
- [ ] Bring USB camera and test YOLO at checkout counter
- [ ] Prepare test script: inflow -> forecast -> schedule -> checkout -> AI query

### During Field Test
- [ ] Collect 1-2 weeks of real sales data
- [ ] Test YOLO accuracy under real lighting and tray conditions
- [ ] Gather staff feedback on POS usability
- [ ] Gather owner feedback on AI Brain recommendations (baking plan, promo, schedule)
- [ ] Log all bugs and UX friction points

### Post Field Test
- [ ] Retrain XGBoost models on real sales data
- [ ] Fine-tune YOLO with real bakery images if needed
- [ ] Adjust S3 constraint model based on actual staffing needs
- [ ] Iterate combo scoring weights based on owner preferences
- [ ] Finalize documentation for final report submission
