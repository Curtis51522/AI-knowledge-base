---
title: "MemoryWAM: Efficient World Action Modeling with Persistent Memory"
authors: "Sizhe Yang, Juncheng Mu, Tianming Wei, Chenhao Lu, Xiaofan Li, Linning Xu, Zhengrong Xue, Zhecheng Yuan, Dahua Lin, Jiangmiao Pang, Huazhe Xu"
date: 2026-06-18
arxiv_id: "2606.20562v1"
categories: cs.RO
tags: [world-action-model, persistent-memory, robotic-manipulation, VLA, memory-augmented-agent]
status: unread
---

# MemoryWAM: Efficient World Action Modeling with Persistent Memory

**链接**: [arXiv](https://arxiv.org/abs/2606.20562v1) | [PDF](https://arxiv.org/pdf/2606.20562v1)

---

## 一句话总结
MemoryWAM 提出了一种混合式持久记忆机制，让世界动作模型（World Action Model）能够在长程机器人操作任务中高效地同时利用短期细节和长期上下文，解决了现有方法在非马尔可夫环境下推理效率与记忆长度之间的根本矛盾。

---

## 核心贡献
1. **混合记忆架构**：创新性地将近期帧、事件边界锚点帧和紧凑的 gist token（摘要令牌）三者结合，分别捕获短期细节、关键事件信号和长期历史信息。
2. **定制化注意力机制**：设计了一种特殊的注意力检索方案，使模型能同时访问详细的短期上下文和压缩的长期上下文，支持基于记忆的决策。
3. **效率突破**：在不牺牲推理延迟和 GPU 内存的前提下，显著超越强 VLA 基线模型在长程、记忆依赖的操控任务上的表现。

---

## 为什么重要（面向AI Agent学习者视角）
1. **Agent 记忆的通用难题**：当前大多数 LLM Agent 和机器人 Agent 都面临 MemoryWAM 试图解决的同一个核心矛盾——长上下文会导致推理成本激增，而短窗口又无法处理非马尔可夫任务。MemoryWAM 的混合记忆设计（gist token + 锚点帧）提供了一个可直接借鉴的工程范式。
2. **VLA 范式的关键进化**：Vision-Language-Action 模型正成为具身智能 Agent 的主流框架，但它们的记忆能力普遍薄弱。MemoryWAM 在 VLA 范式上增加了一个重要的"持久记忆"维度，这对构建长期自主 Agent 具有深远意义。
3. **跨领域迁移潜力**：这种混合记忆设计不仅适用于机器人，对于工具调用型 Agent、对话型 Agent、持续学习系统等需要同时处理短期上下文和长期历史的场景都有直接借鉴价值。

---

## 关键术语
| 术语 | 解释 |
|------|------|
| World Action Model (WAM) | 同时建模视觉预测和动作的模型，以当前和历史观测为条件进行推理 |
| Gist Token | 压缩长期历史信息的紧凑摘要令牌，类似记忆的"摘要"表示 |
| Event-Boundary Anchor Frame | 事件边界的锚点帧，标记关键状态转换的时刻 |
| VLA (Vision-Language-Action) | 视觉-语言-动作模型，将视觉感知、语言指令和动作输出统一建模 |
| Non-Markovian Environment | 非马尔可夫环境，当前状态不足以决定最优动作，需要依赖历史信息 |

---

## 后续关联
- [[LedgerAgent - Structured State for Policy-Adherent Tool-Calling Agents]] —— 同为 Agent 状态管理的工作，MemoryWAM 聚焦记忆效率，LedgerAgent 聚焦策略合规性

---

## 个人笔记
> [待阅读后补充]
