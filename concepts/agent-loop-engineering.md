---
title: Agent Loop Engineering
created: 2026-06-10
updated: 2026-06-10
type: concept
tags: [ai-tools, agent-architecture, agent-loop, react, langchain, hermes-agent, claude-code]
sources: [https://www.anthropic.com/engineering/building-effective-agents, https://lilianweng.github.io/posts/2023-06-23-agent/, https://www.deeplearning.ai/the-batch/how-agents-can-improve-llm-performance/]
confidence: high
contested: false
contradictions: []
---

# Agent Loop Engineering

## 是什么

Agent Loop（智能体循环工程）是 AI Agent 系统的核心架构模式——设计 Agent 如何"感知→思考→行动→观察→循环"的完整运行骨架。

**一句话：300 行代码就能实现一个最小化的 ReAct 循环**（quantumentangled.dev, 2026）。它不是一个产品，而是一个架构模式。

## 最小化实现（ReAct 模式）

```python
while not task_complete:
    thought = llm.think(context + observation)
    action = extract_action(thought)  # 调用工具、搜索、写文件等
    observation = execute(action)
    context += (thought, action, observation)
```

## 核心三要素（Lilian Weng 框架）

1. **Planning（规划）**：任务分解（CoT/ToT）、自我反思
2. **Memory（记忆）**：短期（in-context）+ 长期（外部向量存储）
3. **Tool Use（工具使用）**：调用 API、执行代码、搜索等

## 五大核心循环模式

### 1. ReAct（Reasoning + Acting）
- 最基础、最广泛使用的模式
- 每次循环：Thought → Action → Observation
- 适合 90% 的场景，透明可调试
- 缺点：每次重发全部历史 → 上下文窗口膨胀

### 2. Plan-Execute
- 先制定多步计划 → 逐步执行 → 每步检查是否需要调整
- 变体：Tree-of-Thoughts（多路径探索）、LLM+P（经典 PDDL 规划器）
- 适合复杂多步任务（如代码重构、研究项目）

### 3. Reflexion（反思）
- 执行后自我评估 → 生成书面反思 → 注入下一轮
- 本质："从失败中学习"的增强循环
- Hermes Agent 的技能自进化系统可视为 Reflexion 的高级实现

### 4. Multi-Agent Collaboration
- 多个 Agent 分工协作，共享 Kanban 看板拉取任务
- A2A 通信协议：部分用 TOML 代替 JSON 避免幻觉语法错误
- 适合大规模并行工作流

### 5. Meta-Cognitive（元认知循环）
- 不只是执行任务，还在学习如何更好地执行
- Hermes Agent 独有：Inference → Action → Reflection → Learning
- 每次循环后可以自动创建/修改技能文件

## Andrew Ng 四大 Agentic Design Patterns（2024）

1. **Reflection**：LLM 检查自己的输出并改进
2. **Tool Use**：赋予搜索、代码执行等能力
3. **Planning**：多步计划制定与执行
4. **Multi-Agent Collaboration**：多个 Agent 分工

**关键数据**：GPT-3.5 零样本 HumanEval 48.1%，包在 Agent Loop 中达到 **95.1%**。

## 四大框架对比

| 维度 | Hermes Agent | Claude Code SDK | LangChain AgentExecutor | AutoGPT |
|------|-------------|-----------------|----------------------|---------|
| Loop 类型 | 元认知循环 | API 工具调用循环 | Think-Act-Observe | 自主任务循环 |
| 终止条件 | 模型自决 + token 预算 | stop_reason=end_turn | AgentFinish + max_iterations | 模型自决+用户中断 |
| 上下文管理 | 分层压缩 + ACP 旋转 | Compaction + Prompt Caching | 无内置/Memory 插件 | 压缩策略（新版） |
| 记忆系统 | 技能文件持久化 | 依赖 MCP 记忆工具 | Memory 接口 | 向量数据库 + 文件 |
| 错误恢复 | 自动重试+重新规划 | 依赖开发者实现 | handle_parsing_errors | 自动重试+新路径 |
| 人类介入 | 审批 hook + Transport 层 | Approval hooks | Callback | continuous_mode 开关 |

### Hermes 的独有优势

- 唯一内置"学习"的 loop：每次循环后可以自我修改/创建 skill 文件
- `context_compressor.py` + `context_engine.py` 实现分层上下文压缩
- ACP 协议支持上下文旋转和结构化压缩
- 全量 session 持久化

### LangGraph：AgentExecutor 的进化

LangChain 官方的 AgentExecutor 正被 LangGraph 取代：
- 不再是一个黑盒 while 循环 → 显式有向图（DAG）
- 使用 Pregel 算法做图执行，支持并行和条件分支
- 内置 checkpointing（每步自动保存 → 支持 time travel/重放）
- 原生 Interrupts（人类介入作为一等公民）

## 五个关键工程原则

### 1. 不要过度自主
- 完全自主的 Agent = 死循环 + 幻觉确认 + token 爆炸
- 实践共识：人类介入 + 硬边界 + 预算限制
- 5 次失败迭代后硬停止，防止 token 耗尽

### 2. 上下文窗口是最大成本
- 每次迭代重发完整历史 → token 消耗 ×N
- 模型提供商（OpenAI/Anthropic）从 token 中盈利 → 没有动力帮你省
- 方案：滑动窗口/摘要/结构化记忆
- Neural-Ledger System（2026-04）：124 token 恢复 18,751 token 上下文（99.3% 节省）

### 3. 裸写优先于框架
- Anthropic 明确建议：先用 LLM API 直接写
- 框架抽象层掩盖底层 prompt/response，难以调试
- 等真正需要边界控制时再用 LangGraph

### 4. 简单任务不需要 Agent Loop
- 单次 LLM + RAG 能搞定的别上 Agent
- Agent 用延迟和成本换取任务性能——不是免费的
- "Find the simplest solution first, only add complexity when needed"

### 5. 安全是头等大事
- Agent 每次工具调用都可能泄露数据
- Guardian Runtime：本地防火墙、硬预算自动终止、API key 扫描
- Guestlist 工具：预检目标站点是否允许 Agent 访问（40-60% 站点屏蔽自动化访问）
- 16% 的 Agent 会把 email/password 传给未经授权的服务

## 最新趋势（2025-2026）

1. **Agent Runtime 操作系统化**：不再是简单循环，而是持久化、中断恢复、事件流的完整运行时
2. **浏览器端 Agent Loop**：AG2B 在浏览器中运行循环，减少服务器依赖性
3. **K/V 状态持久化**：跨会话记忆无需重放全部历史
4. **MCP 协议标准化**：工具接口标准协议正在形成生态
5. **深度 Agent**：从简单循环向深层推理图演进

## 推荐阅读

1. [Anthropic: Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents) — 必读
2. [Lilian Weng: LLM Powered Autonomous Agents](https://lilianweng.github.io/posts/2023-06-23-agent/) — 学术级综述
3. [DeepLearning.AI: Agentic Design Patterns](https://www.deeplearning.ai/the-batch/how-agents-can-improve-llm-performance/) — Andrew Ng 四大模式
4. [300-LoC ReAct Loop](https://quantumentangled.dev/viewpost/11/whats-actually-inside-an-ai-agent-a-300-loc-react-loop) — 手把手实现

## 相关概念

- [[last30days-skill]] — Agent Loop 的具体应用：多源搜索的智能循环
- [[Hermes-Agent-三层路由架构设计]] — Hermes 的元认知循环实现
- [[harness-engineering]] — Agent 外部脚手架六层架构
- [[deer-flow-multi-agent]] — 多 Agent 协作循环的实现
