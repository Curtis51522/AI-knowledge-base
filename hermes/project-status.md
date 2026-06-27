# Project Status — Bakery AI System

> Last updated: 2026-06-27 12:15

## Current Phase
**S1 YOLO11s Grid Search 训练中** (用户自己电脑, git-bash, 24 组 × 30 epoch, imgsz=416, batch=16/8)

## Module Status

| Module | Status | Detail |
|--------|--------|--------|
| S1 | 🟡 训练中 | yolo11s, 28类, merged_yolo 数据集, experiments.py 正在跑 Grid Search(24组) |
| S2 | ✅ 完成 | XGBoost 预测 6 款面包 |
| S3 | 🟡 排班完成 | KPI 设计完成(4指标×Z-Score), 签到系统待开发 |
| S4 | 🟡 POS持续改进 | ✅ 支付弹窗(Cash/Card/QR+找零+小票), ✅ 咖啡Hot/Iced+冰量糖量, ⚠️ BM翻译, ❌ 购物车UX(✕删/-+/Clear Cart), ❌ 折扣修复, ❌ Fresh/Day-1分开 |
| S5 | 🟡 方向已定 | Dashboard Intelligence Engine, 6Agent并行不变, 输出管道从聊天框→Dashboard面板 |
| DB | 🟡 schema_v2.sql 已写 | 12张新表(products/orders/order_items/attendance/raw_materials/material_transactions/employee_kpi/material_wastage_log/daily_summary/product_recipes/alert_log), 待执行到MySQL |
| Dashboard | ✅ 4面板设计完成 | 预测(需求/产量/采购)、排班+KPI(出勤/排班/Z-Score排名)、收入(营收/利润/排行/历史)、库存(面包/烘焙材料/咖啡材料) |
| 数据集 | ✅ 完成 | data/merged_yolo/, 28类, ~19k 图(YOLO格式), 含16核心+12菲律宾品类 |
| 产品数据 | 🟡 16款面包 | 6老+10新, 价格+配方已写入schema_v2, 成本为估算值待真实数据 |
| 咖啡 | 🟡 6款 | 已有热/冰+冰量糖量自定义, 配方+成本待补(中国真实数据) |
| 语言 | 🟡 EN/BM | 暂用BM(马来语), 中文待重新实施 |

## 今天已完成 (2026-06-26~27)

1. S1 YOLO 数据集合并 (5个Roboflow → merged_yolo, 28类, 19k图)
2. S1 训练脚本: experiments.py(24组Grid Search+3组消融), full_train.py(200 epoch)
3. S1 baseline: zero-shot 消融 C
4. S1 改写: yolo26m→yolo11s, pretrained=True, mosaic=1.0, YOLO11参数(box/cls/dfl/dropout)
5. S4 支付弹窗: Cash/Card/QR + 找零 + 小票 + closePaymentModal/closeReceipt
6. S4 咖啡自定义: Hot/Iced切换 + 冰量糖量Pill按钮, 变量式onclick(零转义)
7. 4 Dashboard 设计定稿: 预测/排班/收入/库存
8. schema_v2.sql 完善: 16款面包产品+配方, 10张新表
9. KPI 设计: 4指标×Z-Score(出勤率/准时率/工时达标率/团队达标率)
10. 原材料损耗: 每周盘点机制, 默认5%, 自动更新

## 编辑教训

- ❌ **绝不**用 patch() 编辑 index.html JS字符串 — 引号转义必损
- ✅ 用 execute_code + bytes.replace()
- ✅ 用变量式 onclick (_ci, _cn等) 避免嵌套引号
- ✅ 每次改动后验证: 重启服务器 → curl ping → 刷新登录测试
- ❌ 大批量改翻译字典 → 造成重复script块、文件损坏 → git checkout恢复 → 全部改动丢失

## 下一步

1. 等 S1 Grid Search 跑完 → best_config.json → full_train.py
2. 继续 S4: 购物车UX(✕删/-+/Clear Cart), 折扣修复, Fresh/Day-1分开
3. 重新实施中文翻译 (小心: 一个改动一验证)
4. 执行 schema_v2.sql 到 MySQL
5. S5 转型: 6 Agent → Dashboard JSON输出
6. 找中国烘焙销售数据集(替换马来西亚数据)
7. 产品真实成本数据(中国烘焙材料价格)
