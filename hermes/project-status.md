# Project Status
# Managed by Hermes, updated by Codex after execution.

## Active Projects

| Project | Status | Priority | Last Updated | Current Sprint |
|---------|--------|----------|-------------|----------------|
| [[projects/final-report/README|final-report]] | Field Testing & Iteration | High | 2026-06-11 | Offline field test prep |
| [[projects/dl/README\|dl]] | Paper Writing | High | 2026-06-11 | Paper drafting & formatting |

## Project Details

### final-report — Bakery AI System
- **Goal:** Multi-agent AI operations system for a Malaysian bakery-cafe (KL). 6 products, 6 coffee beverages, 10 employees, 2 ovens, 2 checkout counters.
- **Subsystems (all completed):**
  - S1: YOLOv8n visual recognition + OpenCV tray-color classification
  - S2: XGBoost demand forecasting (7-day, with weather integration)
  - S3: OR-Tools CP-SAT shift scheduling (dual-role, sick leave, KPI persistence)
  - S4: POS frontend + combo engine (JWT auth, 5-dim scoring, DeepSeek sales scripts)
  - S5: AI Brain (DistilBERT intent classifier, 6 agents, MIP + DeepSeek synthesis)
- **Known Limitations:** No real sales data yet, YOLO untested with real camera, revenue = RM0, two servers need manual startup
- **Next:** Bring to bakery for real-world testing, gather owner/staff feedback, iterate


### dl — OCT Retinal Image Classification
- **Goal:** OCT retinal image 4-class classification (CNV/DME/DRUSEN/NORMAL) using ConvNeXt-Base vs Swin-Tiny on OCT2017_30K_V2 dataset.
- **Status:** All experiments complete. ConvNeXt test acc 0.9531, Swin-Tiny test acc 0.9562. Swin-Tiny wins on accuracy + speed.
- **Next:** Write academic paper (APU format), embed figures from outputs/, submit final.ipynb + paper.
- **Key files:** `final.ipynb` at `C:\Users\Curtis\Desktop\learningmaterials\SEMESTER3\DL\notebook\final.ipynb`
