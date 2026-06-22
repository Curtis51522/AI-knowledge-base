---
title: "Multi-LCB: Extending LiveCodeBench to Multiple Programming Languages"
authors: "Maria Ivanova, Pavel Zadorozhny, Rodion Levichev, Ivan Petrov, Adamenko Pavel, Ivan Lopatin, Alexey Kutalev, Dmitrii Babaev"
date: 2026-06-18
arxiv_id: "2606.20517v1"
categories: cs.AI, cs.PL
tags: [code-generation, benchmark, multi-language, LLM-evaluation, livecodebench]
status: unread
---

# Multi-LCB: Extending LiveCodeBench to Multiple Programming Languages

**链接**: [arXiv](https://arxiv.org/abs/2606.20517v1) | [PDF](https://arxiv.org/pdf/2606.20517v1)

---

## 一句话总结
Multi-LCB 将广泛使用的代码生成基准 LiveCodeBench 扩展到了 12 种编程语言，通过在 24 个 LLM 上的全面评测，揭示了严重的 Python 过拟合、语言特定污染和多语言性能差异等关键问题。

---

## 核心贡献
1. **跨语言评测基准**：将 LCB 的 Python 评测任务系统性地转换为 12 种编程语言（包括 Python）的等价任务，保留了 LCB 的防污染控制和评估协议。
2. **自动化追踪机制**：与原始 LCB 格式完全兼容，能自动追踪未来 LCB 的更新，实现对跨语言代码生成能力的系统评估。
3. **重要发现**：在 24 个 LLM 上评测后发现：Python 过拟合现象严重、存在语言特异性数据污染、多语言性能差异显著。

---

## 为什么重要（面向AI Agent学习者视角）
1. **Agent 代码生成能力的真实度量**：当前大多数代码生成 Agent（如 Cursor、Copilot 等）虽然在 Python 上表现良好，但在多语言场景下能力严重不均。Multi-LCB 提供了一个更全面的能力评估工具，可以帮助 Agent 开发者找到模型的真实能力边界。
2. **Python 过拟合的警示**：论文揭示的 Python 过拟合现象意味着 Agent 在非 Python 项目中的表现可能远不如预期，这对于构建生产级多语言 Agent 是一个重要提醒。
3. **评测体系的进化方向**：作为 LiveCodeBench 的扩展，Multi-LCB 代表了代码生成评测从单语言向多语言、从静态到动态演进的方向，Agent 开发者也应相应更新自己的评测标准。

---

## 关键术语
| 术语 | 解释 |
|------|------|
| LiveCodeBench (LCB) | 广泛使用的 LLM 代码生成评测基准，通过持续添加新题目来实现防污染评估 |
| Contamination-Aware Evaluation | 防污染评估，通过跟踪题目发布日期来避免训练数据泄漏导致的虚高得分 |
| Python Overfitting | Python 过拟合，模型在 Python 任务上表现显著优于其他语言的现象 |
| Cross-Language Code Generation | 跨语言代码生成，模型在同一算法问题上用不同编程语言实现的能力 |

---

## 后续关联
- [[Execution-State Capsules - Graph-Bound Execution-State Checkpoint and Restore for Low-Latency, Small-Batch, On-Device Physical-AI Serving]] —— 代码生成是 Agent 核心能力，高效的执行状态管理是代码执行的基础

---

## 个人笔记
> [待阅读后补充]
