# Bakery AI System ? Final Report
## Project Goal
Design and implement a multi-agent AI operations system for a medium-sized Malaysian bakery-cafe (Kuala Lumpur). The system integrates computer vision, demand forecasting, shift scheduling, POS checkout with combo recommendations, and a multi-agent AI Brain for real-time decision support.
**Scale:** 6 products, 6 coffee beverages, 10 employees, 2 ovens, 2 checkout counters. Rest day: Monday.
---
## Current Phase: Offline Field Testing & Iteration
The system is fully built and running locally. Next: bring to the bakery for real-world testing, gather feedback from the shop owner/staff, and iterate based on actual operational needs.
---
## Current Progress (Completed)
### S1 ? Visual Recognition (YOLO + OpenCV)
- YOLOv8n trained for 6-product detection
- OpenCV tray-color classification (green = regular, orange = discount zone)
- FIFO inventory deduction at checkout
### S2 ? Demand Forecasting (XGBoost)
- 6 per-product XGBoost quantile regression models
- 7-day forecast with low/median/high bounds
- Weather integration via VisualCrossing API
### S3 ? Shift Scheduling (CP-SAT)
- OR-Tools CP-SAT solver with demand-aware staffing
- Dual-role support, sick leave with auto-replacement, skill-based swap
- Past-date locking + KPI snapshot persistence
### S4 ? POS Frontend + Combo Engine (BFF Architecture)
- Responsive web POS with JWT auth (staff/manager roles)
- 5-dim combo scoring, dynamic discount for Day-1 items
- Checkout with FIFO deduction + receipt, LLM sales scripts (DeepSeek)
### S5 ? AI Brain (Multi-Agent Engine)
- DistilBERT intent classifier (8 intents), 6 programmatic agents
- MIP Pareto plan generation + DeepSeek LLM plan selection & synthesis
- System Alerts: 5-min background monitor (inventory, forecast, schedule, trends)
---
## Known Limitations (Pre-Field-Test)
| # | Issue | Impact |
|---|-------|--------|
| 1 | **No real sales data** | All training on synthetic seed data; forecast accuracy unvalidated |
| 2 | **YOLO not tested with real camera** | Static test images only; real lighting/angles/occlusion unknown |
| 3 | **Revenue = RM0** | Profit agent shows negative margin until real transactions recorded |
| 4 | **Two servers need manual startup** | S5 (:8001) + main (:8002) started separately |
| 5 | **MILP occasionally infeasible** | Graceful fallback to LP + rounding works but is suboptimal |
| 6 | **No bakpia/kitchen integration** | Oven scheduling not yet connected to real equipment |
---
## Next Steps
### Field Test Prep
- [ ] Prepare laptop/deployment environment for on-site testing
- [ ] Seed database with realistic initial inventory
- [ ] Bring USB camera for YOLO testing at checkout counter
- [ ] Prepare test script: inflow ? forecast ? schedule ? checkout ? AI query
### During Field Test
- [ ] Collect real sales data for 1-2 weeks
- [ ] Test YOLO accuracy under real lighting and tray conditions
- [ ] Gather staff feedback on POS usability
- [ ] Gather owner feedback on AI Brain recommendations (bake plans, promo, scheduling)
- [ ] Log all bugs and UX friction points
### Post Field Test
- [ ] Retrain XGBoost models on real sales data
- [ ] Fine-tune YOLO on real bakery images if needed
- [ ] Adjust S3 constraint model based on actual staffing needs
- [ ] Iterate on combo scoring weights per owner preference
- [ ] Polish documentation for final submission
