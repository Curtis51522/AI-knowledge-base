---
tags:
  - bakery
  - agent
  - workspace
  - product
  - idea
date: 2026-06-24
status: idea
---

# Bakery AI Workspace — 烘焙连锁集团 AI Agent Workspace

> 继承 S5 Bakery AI System，扩展为多分店集团化管理平台

---

## 🎯 产品定位

基于现有 S5 多 agent 系统的烘焙连锁集团 AI 协作平台。Yooclaw 风格 workspace 界面，管理者通过拖拽 agent 完成预测、排班、补货等任务，agent 结果存入飞书/Obsidian 文档。

## 👥 用户角色

| 角色 | 权限 | 
|------|------|
| **集团管理者** | 查看所有分店、审批超阈值决策、跨店 AB 对比 |
| **分店店长** | 只看自己分店，日常决策自行确认 |

## 🖥️ 核心交互

```
打开 Workspace
    ↓
左侧分店列表（KL / Cheras / PJ ...）
    ↓
点击分店名 → 展开该店的 6 个 agent
    ↓
拖拽 Demand Agent 到中间画布
    ↓
输入预测日期范围 → agent 显示预测曲线图
    ↓
确认 → 自动生成文档（飞书/Obsidian）→ 保存
```

## 🔄 审批流程（折中方案）

```
分店预测 → 确认
    ↓
超阈值？（偏差 > ±30% vs 集团预期）
   /        \
  否         是
   |          ↓
 自动确认   集团审核
   |          ↓
  写入分店   审批后归档
```

> 日常波动分店自决，偏离集团预期自动触发审批。避免过度审核拖慢效率，同时保留集团管控权。

## 🏗️ 多分店架构

- 现有 6 个 agent 逻辑不改
- 数据库加 `branch_id` 字段隔离分店数据
- 每家分店有独立 agent 实例（Demand_Klang、Demand_Cheras …）
- Workspace 层通过分店选择器切换上下文

## 🧠 底层 AI（继承 S5）

| Agent | 功能 | 
|-------|------|
| Demand Agent | 销量预测 |
| Inventory Agent | 库存管理 |
| Production Agent | 生产计划 |
| Staffing Agent | 排班 |
| Promo Agent | 促销推荐 |
| Profit Agent | 利润分析 |

每个 agent 按 `branch_id` 过滤数据，剩余逻辑复用现有代码。

## 📅 路线（初步）

| 阶段 | 内容 |
|------|------|
| Phase 1 | 已有 S5 → 单店版稳定，明天 bakery demo |
| Phase 2 | 数据库加 branch_id，扩展为多分店版 |
| Phase 3 | 构建 Yooclaw 风格 Workspace 前端 |
| Phase 4 | 对接飞书/Obsidian 文档输出 |
| Phase 5 | 审批流程 + 跨店 AB 对比 |

---

## 关联

- 底层项目：[[projects/final-report/README.md|Bakery AI System - Final Report]]
- 当前状态：明天 bakery demo（June 25），Product idea 阶段
