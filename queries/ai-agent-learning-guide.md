---
title: AI Agent 开发学习路线
created: 2026-05-18
updated: 2026-06-10
type: query
tags: [ai-tools, agent, learning, guide, claude-code, skills, mcp, agent-loop]
confidence: high
contested: false
contradictions: []
---

# AI Agent 开发学习路线

> 面向非程序员/创作者的 Agent 开发入门指南。不需要精通编程，但需要理解 Agent 的思维方式。

---

## 第一层：理解 Agent 是什么（先看这个）

### 必读概念

| 概念 | 一句话 | 详见 |
|------|--------|------|
| **Agent** | 能自主使用工具、做决策、完成多步任务的 AI | [[AI-Agent-核心概念对照]] |
| **Agent Loop** | Thought → Action → Observation 循环，Agent 的"呼吸" | [[agent-loop-engineering]] |
| **Tool** | Agent 的手——搜索、读文件、执行命令 | [[AI-Agent-核心概念对照]] |
| **Context** | Agent 的"视野"——System Prompt + 对话历史 + 工具输出 | [[claude-md-optimization]] |
| **Memory** | Agent 跨 session 记住的事情 | [[AI-Agent-核心概念对照]] |

### ⭐ 新增：Agent Loop 专题（必读）

了解 Agent Loop 不只是知道"循环"这个词——它是 Agent 工程最核心的架构模式。2026 年 6 月硅谷爆火的 **Loop Engineering** 正在改变 AI 工程的方式。

| 阅读顺序 | 内容 | 适合 |
|---------|------|------|
| 1️⃣ | [[agent-loop-engineering]] | 全景理论：5 大模式 + 4 大框架对比 + 5 条工程原则 |
| 2️⃣ | [[agent-loop-清华鑫哥]] | 视频笔记：5 步设计法 + 6 种拓扑 + 7 大实战场景 |
| 3️⃣ | [[last30days-skill]] | 实战案例：Agent Loop 在多源搜索中的完整实现 |

**关键认知**：GPT-3.5 零样本得分 48.1%，包在 Agent Loop 中达到 **95.1%**（Andrew Ng, 2024）。Loop 比模型本身更重要。

### 必读文章（按顺序）

1. **Anthropic: Building Effective Agents** — 最权威的 Agent 入门
   https://www.anthropic.com/engineering/building-effective-agents
   
2. **OpenAI: A Practical Guide to Building AI Agents** — 生产级实践
   https://platform.openai.com/docs/guides/agents
   
3. **Martin Fowler: Harness Engineering** — 理解 Agent 脚手架
   https://martinfowler.com/articles/harness-engineering.html

4. **Lilian Weng: LLM Powered Autonomous Agents** — 学术级综述
   https://lilianweng.github.io/posts/2023-06-23-agent/

---

## 第二层：写你的第一个 Skill（动手）

Skill 是 Agent 的可复用能力单元。一个 Skill 就是告诉 Agent：「遇到这类任务时，这样做」。

### 最简单的 Skill 结构

```markdown
---
name: my-first-skill
description: 当用户说 X 时触发
---

# My First Skill

## 触发条件
- 用户提到 "xxx"

## 操作步骤
1. 先做 A
2. 再做 B
3. 输出 C

## 注意事项
- 坑1：xxx
- 坑2：yyy
```

### 实战：拆解一个真实 Skill

我们知识库里已分析的 Skill：

| Skill | 用途 | 复杂度 |
|-------|------|--------|
| `last30days-skill` | 12 平台跨源搜索，Agent Loop 的经典实现 | ⭐⭐⭐⭐ |
| `cheat-on-content` | 内容创作校准（14 子 Skill） | ⭐⭐⭐⭐ |
| `weread-cli` | 微信读书操作 | ⭐⭐ |

**练习**：
- 读 `cheat-on-content` 的 [[cheat-on-content|完整分析]]，理解闭环 Skill 的设计
- 读 `last30days-skill` 的 [[last30days-skill|完整分析]]，理解 Agent Loop 如何在真实项目中落地——**这个案例完美展示了 Agent Loop 的"感知→思考→行动→观察"**

### 写 Skill 的核心原则

1. **一个 Skill 只做一件事** — 别写成瑞士军刀
2. **触发条件明确** — Agent 需要知道什么时候用它
3. **步骤可执行** — 每一步 Agent 都能用已有工具完成
4. **有坑就写** — 已知问题不写进 Skill，Agent 会重复踩
5. **先跑通再优化** — 别追求完美，先用起来

---

## 第三层：理解 Agent 的"手脚"——工具与 MCP

### 工具设计的灵魂

> **"工具设计就是 Agent UX"** —— Anthropic

工具是 Agent 和外部世界交互的唯一方式。设计工具 = 设计 Agent 的"手"。

**好工具 vs 坏工具**：
- ✅ 名字清晰：`search_files` 而非 `sf`
- ✅ Schema 完整：参数类型、必填/可选、默认值
- ✅ 错误友好：返回人类可读的错误信息
- ❌ 名字模糊：Agent 猜不出这工具干什么
- ❌ 参数不明：Agent 不知道传什么

### MCP（Model Context Protocol）

MCP 是标准化的工具注册协议。Agent 通过 MCP 发现可用工具。

- [[claude-code-mcp-browser]] — 实战：通过 MCP 让 Claude Code 控制浏览器

---

## 第四层：Context Engineering（上下文工程）

### Agent 能看到什么？

```
┌──────────────────────────────────────┐
│ System Prompt（你是谁、能做什么）      │
├──────────────────────────────────────┤
│ CLAUDE.md / Rules（项目规范）          │
├──────────────────────────────────────┤
│ 对话历史（之前说了什么）               │
├──────────────────────────────────────┤
│ 当前消息（用户说了什么）               │
├──────────────────────────────────────┤
│ 工具输出（工具返回了什么）             │
└──────────────────────────────────────┘
                              ↓
                    全部塞进 Context Window
```

### 核心原则

1. **少即是多** — CLAUDE.md 超 200 行 Agent 会变蠢
2. **按需注入** — 不要把所有信息一次性塞进去
3. **结构化** — 用 markdown 标题、列表、表格，Agent 解析更快

详见：[[claude-md-optimization]]

---

## 第五层：Harness Engineering（驾驭工程）+ Loop Engineering

### 这才是真正的门槛

Prompt Engineering 让 Agent 听懂你。
Context Engineering 让 Agent 看到该看的。
**Harness Engineering 让 Agent 持续、可靠地完成任务。**
**Loop Engineering 让 Agent 高效、可控地运转。**

两者是 **"外部装备"和"内部逻辑"** 的关系：

| 维度 | Harness Engineering | Loop Engineering |
|------|-------------------|-----------------|
| 关注什么 | Agent 周围有什么工具、权限、记忆 | Agent 内部怎么思考、执行、循环 |
| 六个层次 | 1.上下文 2.工具 3.编排 4.记忆 5.评估 6.约束 | 1.停止条件 2.上下文 3.执行捕获 4.反馈闭环 5.护栏 |
| 核心问题 | Agent 能用什么？谁在看？ | Agent 怎么跑？什么时候停？ |
| 详见 | [[harness-engineering]] | [[agent-loop-engineering]] |

### 清华鑫哥的总结（来自抖音视频）

> Loop Engineering = 把"人"从 Agent 的执行循环中剥离出来。Skills 比 Prompt 更重要，Sub-agents 是用来检查你不是帮你干活。

详见：[[agent-loop-清华鑫哥]]

### 六层 Harness 架构

```
6. 约束校验 & 恢复  ← 权限、Hook、沙盒
5. 评估 & 观测      ← 追踪每一步决策
4. 状态 & 记忆      ← 跨 session 持久化
3. 执行编排         ← Agent Loop 设计 ← Loop Engineering 的核心
2. 工具系统         ← 工具注册与调用
1. 上下文管理       ← 按需注入与压缩
```

详见：[[harness-engineering]]

---

## 推荐学习项目（由浅入深）

### 入门级：看别人怎么写

| 项目 | 为什么值得学 |
|------|------------|
| [mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill) | 37K⭐，Agent Loop 在多源搜索中的最佳实践——边学边用 |
| [ai-boost/awesome-harness-engineering](https://github.com/ai-boost/awesome-harness-engineering) | 978⭐，Agent 脚手架全景图 |
| [shiquda/weread-cli](https://github.com/shiquda/weread-cli) | 小而美，一个 Skill 配一个 CLI |
| [XBuilderLAB/cheat-on-content](https://github.com/XBuilderLAB/cheat-on-content) | 14 个 Skill 的完整闭环 |

### 进阶级：理解源码

| 项目 | 为什么值得学 |
|------|------------|
| [ZhangHanDong/harness-engineering-from-cc-to-ai-coding](https://github.com/ZhangHanDong/harness-engineering-from-cc-to-ai-coding) | 1.3K⭐，《马书》——逆向 Claude Code 源码 |
| [stablyai/orca](https://github.com/stablyai/orca) | 2.7K⭐，多 Agent 并行 IDE，理解编排 |
| [aaif-goose/goose](https://github.com/aaif-goose/goose) | 48K⭐，开源 AI Agent 框架——看 Rust 实现的 Agent Loop |

### 实战级：自己造

| 方向 | 做法 |
|------|------|
| 装一个 last30days | `/last30days <话题>` 体验 Agent Loop 在真实场景中的威力 |
| 写一个 Skill | 从你日常重复的工作中挑一个，写成 Skill |
| 设计 Agent Loop | 画你的 Agent 的 Thought→Action→Observation 流程 + 停止条件 + 护栏 |

---

## 学习节奏建议（更新版）

```
Week 1-2：读完「第一层」所有文章 + 理解 Agent Loop
         → 重点看 [[agent-loop-engineering]] + [[agent-loop-清华鑫哥]]
         → 关键认知：Loop 比模型更重要（GPT-3.5: 48% → 95%）
Week 3-4：装 last30days 体验真实 Agent Loop + 写第一个 Skill
Week 5-6：深入 Harness Engineering + Loop Engineering，理解"外部装备"和"内部逻辑"的关系
Week 7-8：设计自己的 Agent 系统，画出完整 Loop 图
```

---

## 速查表

### Agent 开发工具箱

| 工具 | 用途 |
|------|------|
| Claude Code | Agent CLI，支持 Skill、Hook、子 Agent |
| Codex | OpenAI 的 Agent CLI |
| Goose | 48K⭐ 开源 Agent 框架（Rust） |
| Orca | 多 Agent 并行 IDE |
| MCP | 工具注册协议 |
| last30days | 37K⭐ Agent Loop 实战工具（跨源搜索） |

### 关键术语

| 术语 | 含义 |
|------|------|
| Agent Loop | Thought → Action → Observation 循环 |
| Loop Engineering | 设计 Agent 如何高效、可控地循环的工程学科 |
| Skill | Agent 的可复用能力单元 |
| Tool | Agent 调用的外部功能 |
| MCP | 标准化工具注册协议 |
| Context Window | Agent 一次能"看到"的全部内容 |
| Harness | Agent 的外部脚手架 |
| Hook | 拦截 Agent Loop 的事件钩子 |
| Sub-agent | 负责检查/验证/评分的辅助 Agent |
| ReAct | 最基础的 Agent Loop 模式：Reasoning + Acting |

---

## 参见

- [[AI-Agent-核心概念对照]] — 八个核心概念一张表
- [[agent-loop-engineering]] — Agent Loop 全景：5 大模式 + 4 大框架对比
- [[agent-loop-清华鑫哥]] — 清华鑫哥视频笔记：5 步设计法 + 6 种拓扑 + 7 大场景
- [[last30days-skill]] — Agent Loop 实战案例：多源搜索的完整实现
- [[harness-engineering]] — Agent 脚手架六层架构
- [[claude-md-optimization]] — Context 注入文件优化
- [[cheat-on-content]] — 14 个 Skill 的实战拆解
- [[claude-code-mcp-browser]] — MCP 实战案例
