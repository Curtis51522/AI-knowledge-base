---
tags: [final-report, kpi-system]
created: 2026-06-27
---

# KPI System — Full Architecture

## Overview

Multi-module employee performance management for 4 roles (baker, barista, cashier, manager).
3-step fairness pipeline: Z-Score normalization -> BSC weighted aggregation -> cross-role unified ranking.

References: [[employee-KPI-normalization-research]] | [[kpi-research]]

## Architecture

| # | Module | File | Role |
|---|--------|------|------|
| 1 | Config | kpi/config.py | Role definitions, BSC weights, KPI catalog |
| 2 | Calculator | kpi/calculator.py | 3-step pipeline: Z-Score -> BSC -> Ranking |
| 3 | Attendance | kpi/attendance.py | Punch card + monthly/weekly metrics |
| 4 | Shift | kpi/shift.py | 7-day auto-scheduler with coverage check |
| 5 | AHP | kpi/ahp.py | Saaty pairwise comparison -> weights (CR < 0.10) |
| 6 | Collector | kpi/collector.py | POS/sales/inventory data gathering |
| 7 | Demo | kpi/demo.py | Full 6-module integrated pipeline |

## Module Details

### 1. Config (config.py)

4 roles x 5 KPIs each (Mambetakunova 2026: 5-7 KPIs per role):

| Role | KPIs |
|------|------|
| Baker | daily_output, waste_rate, product_quality, punctuality, cross_skills |
| Barista | drinks_per_hour, customer_satisfaction, waste_rate, punctuality, latte_art_skill |
| Cashier | checkout_speed, accuracy_rate, upselling_rate, customer_satisfaction, punctuality |
| Manager | team_profit_margin, sales_growth, inventory_accuracy, staff_retention, customer_satisfaction |

BSC dimension weights (AHP-calibrated, CR=0.0038):
Financial: 22.7% | Customer: 22.7% | Internal Process: 42.3% | Learning & Growth: 12.3%

### 2. Calculator (calculator.py)

3-step pipeline:
1. **Z-Score within role**: z = (x - mu) / sigma, invert for "lower_better" KPIs
2. **BSC weighted sum**: S = sum(w_k * z_k) per dimension then aggregate
3. **Cross-role ranking**: all 9 employees ranked by S on unified scale

Outputs: rank, percentile, BSC dimension breakdown, strengths/weaknesses (top-2 Z scores).

### 3. Attendance (ttendance.py)

- PIN-based punch in/out
- Real-time daily status: on_time / late / absent
- Weekly grid (Mon-Sun) with per-day status
- Monthly metrics: attendance_rate, punctuality_rate, absent_days

### 4. Shift Scheduler (shift.py)

4 shift types: OPEN(06:00-14:00), MID(10:00-18:00), CLOSE(14:00-22:00), FULL(08:00-18:00)

Minimum staffing:
OPEN: 2 baker + 1 barista | MID: 1 barista + 1 cashier | CLOSE: 1 barista + 1 cashier | FULL: 1 manager

Auto round-robin balancing, coverage gap detection.

### 5. AHP (hp.py)

Saaty 1-9 pairwise comparison matrix -> eigenvector weights.
Consistency check: CI = (lambda_max - n) / (n-1), CR = CI / RI, must be < 0.10.
Supports manager recalibration via flat upper-triangle input.

### 6. Collector (collector.py)

Gathers raw KPI from:
- Attendance records -> attendance_rate, punctuality
- POS sales -> upselling_rate, checkout_speed, sales_growth
- Inventory -> waste_rate, inventory_accuracy, daily_output
- Manager ratings -> product_quality, customer_satisfaction, cross_skills, latte_art_skill, staff_retention

Falls back to realistic simulation when real data unavailable.
Generates 6-month trend data for charts.

### 7. Integrated Demo (demo.py)

Run: python kpi/demo.py --save kpi/outputs/dashboard.json

Outputs dashboard-ready JSON matching [[dashboard-designs]] Shift+KPI Dashboard:
- Panel 1: Today attendance (real-time punch status)
- Panel 2: Weekly shift grid
- Panel 3: Monthly KPI cross-role ranking
- Role averages + 6-month trend

## Dashboard Output Fields

`
{
  generated_at: ISO timestamp,
  panel_1_attendance: {date, total, present, absent, late, employees[]},
  panel_2_shift: {week_start, week_end, employees[], coverage_ok},
  panel_3_kpi: {month, total_employees, top_performer, ranking[]},
  role_breakdown: {role: {name, avg_score, top}},
  trends: [{month, avg_score, top} x 6 months]
}
`

## Key Design Decisions

1. **Within-role Z-Score first** — eliminates cross-role unit differences before BSC aggregation (Fisher 1925; Purwanto & Asbari 2021)
2. **AHP for weights** — not subjective assignment; CR<0.10 ensures mathematical consistency (Yu 2025; Shi & Wang 2020)
3. **BSC four dimensions** — prevents single-dimension bias (Kaplan & Norton 1992)
4. **5 KPIs per role** — empirical optimum for food service (Mambetakunova 2026)
5. **Unified ranking** — same scale enables cross-role comparison (Zhou et al. 2012)

## Research Citations

* Kaplan, R.S. & Norton, D.P. (1992). Balanced Scorecard. Harvard Business Review
* Saaty, T.L. (1980). The Analytic Hierarchy Process
* Fisher, R.A. (1925). Statistical Methods for Research Workers (Z-Score)
* Yu (2025). Employee Performance Appraisal Based on AHP. ASS. DOI:10.12677/ass.2025.149812
* Shi & Wang (2020). KPI+BSC+AHP Integrated Method. J. Phys. Conf. Ser. DOI:10.1088/1742-6596/1634/1/012058
* Zhou et al. (2012). Multi-Role-Based Appraisal Method. Adv. Mat. Res. DOI:10.4028/www.scientific.net/amr.628.63
* Mambetakunova (2026). KPI System for Food Service
* Purwanto & Asbari (2021). Procedural > Outcome Fairness in Appraisal
* Muhammad et al. (2025). Fairness Mediation in Performance Evaluation

