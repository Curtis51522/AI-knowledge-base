---
title: "LedgerAgent: Structured State for Policy-Adherent Tool-Calling Agents"
authors: "Md Nayem Uddin, Amir Saeidi, Eduardo Blanco, Chitta Baral"
date: 2026-06-18
arxiv_id: "2606.20529v1"
categories: cs.AI, cs.CL
tags: [agent, tool-calling, policy-adherence, state-management]
status: unread
---

# LedgerAgent: Structured State for Policy-Adherent Tool-Calling Agents

**链接**: [arXiv](https://arxiv.org/abs/2606.20529v1) | [PDF](https://arxiv.org/pdf/2606.20529v1)

---

## 一句话总结

传统 Agent 把「任务状态」混在 Prompt 里，导致 Agent 可能读到过时/错误的信息，做出违反策略的 Tool Call。LedgerAgent 把「任务相关状态」分离出来存在一个独立的 **Ledger（账本）** 中，每次做 Tool Call 前都根据 Ledger 检查策略约束，避免违规。

---

## 核心贡献

1. **状态 → Prompt 分离**：将观察到的任务状态（事实、标识符、约束、条件）维护在独立的 Ledger 中，而不是混在 Prompt 里
2. **策略约束检查**：在执行修改环境的 Tool Call 之前，先用 Ledger 中的状态检查是否符合领域策略
3. **推理时方法**：不需要训练，只在推理时增加了一个「检查步骤」——对现有的 LLM 直接可用

### 与传统 Agent 对比

```
传统 Agent（你正在用的方式）:
  User → Prompt(含历史+工具返回+策略) → LLM → Tool Call
  
LedgerAgent:
  User → Prompt(含历史+工具返回) → LLM → 
  [Ledger 检查策略约束] → 符合？→ Tool Call
                         不符合？→ 拒绝并提示
```

---

## 为什么重要（对你的学习）

这篇论文恰好讲的是你**现在正在 Hermes 里做的事情**——Agent 怎么管理多轮对话中的状态信息、怎么判断该不该调用工具。

Ledger 的思路其实就是 **「显式记忆」**——这是我前面说的 Agent 三大组件之一（LLM + 工具 + 记忆/状态）。这篇论文给了这个组件一个具体的实现方案。

---

## 关键术语

| 术语 | 解释 |
|------|------|
| Tool-Calling Agent | 会调用外部工具（API、数据库等）的 LLM Agent |
| Policy Adherence | Agent 的行为要符合业务规则（如「>1000元订单需经理审批」） |
| Task State | 当前任务相关的所有事实（用户是谁、订单到哪一步了等） |
| Ledger | 一种结构化的短期记忆，记录任务状态 |

---

## 后续关联

- [[ReAct: Synergizing Reasoning and Acting]] —— Agent 循环的奠基之作
- [[Toolformer]] —— LLM 学会用工具的早期工作
- 相关的 Agent 安全方向: [[Sovereign Execution Brokers]]（Agent 权限控制）

---

## 个人笔记

> [待阅读后补充：这个方法跟 Hermes Agent 的 memory 系统对比如何？能用在我们的烘焙项目 S5 Agent 上吗？]
