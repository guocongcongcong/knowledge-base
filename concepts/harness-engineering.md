---
title: Harness Engineering（驾驭工程）
created: 2026-05-18
updated: 2026-05-18
type: concept
tags: [ai-tools, agent, architecture, harness-engineering, context-engineering, claude-code]
sources:
  - https://github.com/ai-boost/awesome-harness-engineering
  - https://github.com/ZhangHanDong/harness-engineering-from-cc-to-ai-coding
  - https://martinfowler.com/articles/harness-engineering.html
confidence: high
contested: false
contradictions: []
---

# Harness Engineering（驾驭工程）

## 一句话定义

> **Harness Engineering 是设计 AI Agent 外部脚手架（scaffolding）的工程学科。它决定了 Agent 在真实任务中是成功还是失败 —— 模型是引擎，Harness 是整辆车。**

类比：Prompt Engineering 让模型听懂你 → Context Engineering 让模型看到该看的 → Harness Engineering 让模型持续、可靠、按目标完成任务。

## 为什么重要

**同样的 GPT-4/Claude 模型，不同团队做的 Agent 表现天差地别——答案不在模型参数里，在包裹模型的执行骨架（Harness）里。**

Anthropic 2026 报告：仅 harness 配置差异就能让 benchmark 波动 **5+ 个百分点**。

## 六大层级（经典框架）

### 1. 结构化上下文管理 (Context Delivery)
- 不是把所有东西都塞进 prompt
- 按需注入上下文，自动压缩（/compact）
- 目录地图、时间预算警告、历史对话摘要
- 文件系统优于专用工具（Microsoft 经验：Intent Met 从 45% → 75%）

### 2. 工具系统设计 (Tool Design)
- 工具命名、Schema 设计、错误面——**工具设计就是 Agent UX**
- 命名模糊 → Agent 选错工具；Schema 不完整 → Agent 传错参数
- MCP 协议作为标准化工具注册层

### 3. 执行编排引擎 (Agent Loop / Orchestration)
- ReAct 模式：Thought → Action → Observation 循环
- 五种循环架构：Agent Loop / Event-driven / State-machine / Graph / Hybrid
- 60% 的开源 Agent 项目采用 Agent Loop 模式
- Claude Code 内部：五阶段渐进压缩 + 27 种事件 Hook 管线

### 4. 状态与记忆管理 (Memory & State)
- 跨 session 持久化：Plan.md / Implement.md 等治理制品
- 文件系统作为 Agent 协作面
- 运行时持久化对齐模型训练时语义（否则 80% 丢失变量错误或 3.5× token 开销）

### 5. 独立评估与观测 (Verification & Observability)
- LLM-as-judge 用于推理层验证
- 确定性验证（lint、test）用于计算层
- 追踪 Agent 每一步决策，可审计

### 6. 约束校验与恢复机制 (Permissions & Recovery)
- 权限体系（YOLO 分类器、Hooks、沙盒）
- 防御纵深 5 层安全
- 休眠/唤醒检查点（Meta 方案：6 小时任务中断后恢复不丢上下文）

## Harness Engineering 的权威来源

| 来源 | 核心观点 |
|------|---------|
| **OpenAI** (Codex) | Harness 是让 Agent 可靠运行的脚手架；引入 Plan.md / Implement.md 制品 |
| **Anthropic** (Claude Code) | Agent 不是 workflow；每个 harness 组件都在假设"模型做不到某事"——这些假设会过期 |
| **Google** (ADK) | 多 Agent 拓扑 + 工具注册模型 + 评估管线 |
| **Martin Fowler** | 三系统：Context Engineering + Architectural Constraints + Entropy Management |
| **Microsoft** (Azure SRE Agent) | 35,000+ 生产事故自治处理；文件系统上下文 > 专用工具 |
| **LangChain** | Harness 五项基石：Filesystem / Code Execution / Sandbox / Memory / Context Management |
| **Meta** (CCA) | 三视角设计：AX(Agent体验) / UX(用户) / DX(开发者) |
| **Red Hat** | AI 写更好的代码——当你设计好它工作的环境时 |

## Harness 的"退化设计"原则

> **最好的 Harness 组件设计时就知道它们会随着模型进步而变得不必要。**

每一个 harness 组件都是在补模型的短板。当模型能力提升后，该组件应该能被移除，而不是成为技术债。

## Claude Code 的 Harness 架构（《马书》核心发现）

ZhangHanDong 通过逆向 Claude Code v2.1.88 源码揭示了：

1. **Agent Loop 与工具执行编排**：完整的 ReAct 循环实现
2. **系统提示词与工具提示词**：模型特定调优
3. **Token 预算与 Prompt Cache**：自动压缩、微压缩
4. **权限模式**：YOLO 分类器、规则系统、Hooks（27 种事件类型）
5. **多 Agent 编排**：子 Agent 隔离 + 重建权限上下文
6. **五阶段渐进压缩**：budget reduction → snip → microcompact → context collapse → auto-compact
7. **Feature Flags**：未发布能力管线

## 关键概念对照

| 概念 | 定义 | 层级 |
|------|------|------|
| Prompt Engineering | 让模型理解任务 | 表层 |
| Context Engineering | 让模型看到该看的 | 中层 |
| Harness Engineering | 让模型持续可靠完成任务 | 底层 |
| Agent Loop | Thought→Action→Observation 循环 | 执行核心 |
| MCP | 标准化工具注册协议 | 工具层 |
| Skills | 可复用的 Agent 能力单元 | 能力层 |
| Hooks | 拦截 Agent 循环的事件钩子 | 安全层 |
| Sandbox | 隔离执行环境 | 安全层 |
| Plan.md | 任务规划持久化制品 | 状态层 |

## 参见

- [[claude-md-optimization]] — CLAUDE.md 优化策略（Context Engineering 实践）
- [[AI-Agent-核心概念对照]] — Prompt / System Prompt / Soul / Memory / Skill / Tool / MCP
- [[deer-flow-multi-agent]] — 多 Agent 编排的实践案例
