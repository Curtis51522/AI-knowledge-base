# Dashboard Designs — 已定稿

## 预测 Dashboard ✅ 已定

三块面板：

### 1. 需求预测
- S2 XGBoost 7 天预测栅格（产品×日期）
- ↑↓ 标记变动方向
- DemandAgent 自然语言解释（只标异常）
- 周一店休用 `—`

### 2. 产量建议
- 需求 × 1.05（5% 损耗缓冲）
- 7 天栅格
- ProductionAgent 产量建议 + 原因

### 3. 原材料采购预测
- 下周产量 × 配方(product_recipes) × (1+上周损耗率) - 当前库存
- 损耗率来自 material_wastage_log，默认 5%，每周店长盘点一次自动更新
- S5 输出采购建议 + 预警分级：
  - 🔴 紧急：库存 < 用量×50%
  - ⚠️ 采购：库存 < 用量
  - ✅ 充足：库存 ≥ 用量

### 数据源
- S2 预测表、product_recipes、raw_materials、material_wastage_log
- S5 DemandAgent + ProductionAgent + Arbitrator + LLM 合成 → Dashboard

---

## 排班+KPI Dashboard ✅ 已定

三块：
1. 今日出勤（实时打卡状态）
2. 本周排班（7 天栅格）
3. 本月 KPI（出勤率/准时率/工达标率/团队达标率 × Z-Score 排名）

数据源：attendance、S3 shift_schedule、employee_kpi、S2 forecast + orders

---

## 收入 Dashboard ✅ 已定

五块面板：

### 1. 关键数字（实时）
- 今日营收 / 今日利润 / 今日单量 / 客单价
- 利润 = order_items.line_profit 汇总

### 2. 支付构成 + 品类占比
- 支付：Cash / Card / QR（orders.payment_method）
- 品类：🍞面包 vs ☕咖啡（order_items.product_name）

### 3. 今日销量排行
- 产品 × 销量 × 金额 × 利润
- 数据源：orders + order_items，当天过滤

### 4. 利润趋势（本周 7 天）
- 面包 vs 咖啡分拆
- S5 ProfitAgent 解释

### 5. 历史销量查询
- 日期区间选择 [◀ ▶] + 粒度 [日/周/月]
- 产品 × 销量 × 营收 × 利润 × 占比
- 数据源：GROUP BY product_name, DATE(order_time)

---

## 库存 Dashboard ✅ 已定

三块面板：

### 1. 面包成品库存
- 数据源: batch_inventory
- 分类: Fresh / Day-1 / 总计
- 状态标记: ✅ 充足 / ⚠️ 不足

### 2. 烘焙原材料
- 数据源: raw_materials
- 扣料: 面包师扫 Fresh Batch → product_recipes × 数量
- 显示当前库存 + 补货点阈值

### 3. 咖啡原材料
- 数据源: raw_materials
- 扣料: POS 结账 → product_recipes × 数量
- 同原材料表，按类别过滤显示

S5 解释: 库存不足预警 + 优先销售建议

---

# 全部 Dashboard 汇总

| Dashboard | 面板数 | 数据源 | S5 Agent |
|-----------|--------|--------|----------|
| 预测 | 3 (需求/产量/采购) | S2 + product_recipes + wastage_log | DemandAgent + ProductionAgent |
| 排班+KPI | 3 (出勤/排班/KPI) | attendance + shift_schedule + employee_kpi | StaffingAgent |
| 收入 | 5 (关键数字/支付构成/排行/趋势/历史) | orders + order_items + daily_summary | ProfitAgent |
| 库存 | 3 (面包成品/烘焙材料/咖啡材料) | batch_inventory + raw_materials | InventoryAgent |
