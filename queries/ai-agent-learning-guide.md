---
title: AI Agent 开发学习路线
created: 2026-05-18
updated: 2026-05-18
type: query
tags: [ai-tools, agent, learning, guide, claude-code, skills, mcp]
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
| **Agent Loop** | Thought → Action → Observation 循环，Agent 的"呼吸" | [[harness-engineering]] |
| **Tool** | Agent 的手——搜索、读文件、执行命令 | [[AI-Agent-核心概念对照]] |
| **Context** | Agent 的"视野"——System Prompt + 对话历史 + 工具输出 | [[claude-md-optimization]] |
| **Memory** | Agent 跨 session 记住的事情 | [[AI-Agent-核心概念对照]] |

### 必读文章（按顺序）

1. **Anthropic: Building Effective Agents** — 最权威的 Agent 入门
   https://www.anthropic.com/engineering/building-effective-agents
   
2. **OpenAI: A Practical Guide to Building AI Agents** — 生产级实践
   https://platform.openai.com/docs/guides/agents
   
3. **Martin Fowler: Harness Engineering** — 理解 Agent 脚手架
   https://martinfowler.com/articles/harness-engineering.html

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
| `cheat-on-content` | 内容创作校准（14 子 Skill） | ⭐⭐⭐⭐ |
| `weread-cli` | 微信读书操作 | ⭐⭐ |
| `routing` | 中文关键词→Skill 映射 | ⭐ |

**练习**：读 `cheat-on-content` 的 [[cheat-on-content|完整分析]]，理解它是如何把「内容判断」变成一个闭环 Skill 的。

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

## 第五层：Harness Engineering（驾驭工程）

### 这才是真正的门槛

Prompt Engineering 让 Agent 听懂你。
Context Engineering 让 Agent 看到该看的。
**Harness Engineering 让 Agent 持续、可靠地完成任务。**

六层架构：

```
6. 约束校验 & 恢复  ← 权限、Hook、沙盒
5. 评估 & 观测      ← 追踪每一步决策
4. 状态 & 记忆      ← 跨 session 持久化
3. 执行编排         ← Agent Loop 设计
2. 工具系统         ← 工具注册与调用
1. 上下文管理       ← 按需注入与压缩
```

详见：[[harness-engineering]]

---

## 推荐学习项目（由浅入深）

### 入门级：看别人怎么写

| 项目 | 为什么值得学 |
|------|------------|
| [ai-boost/awesome-harness-engineering](https://github.com/ai-boost/awesome-harness-engineering) | 978⭐，Agent 脚手架全景图 |
| [shiquda/weread-cli](https://github.com/shiquda/weread-cli) | 小而美，一个 Skill 配一个 CLI |
| [XBuilderLAB/cheat-on-content](https://github.com/XBuilderLAB/cheat-on-content) | 14 个 Skill 的完整闭环 |

### 进阶级：理解源码

| 项目 | 为什么值得学 |
|------|------------|
| [ZhangHanDong/harness-engineering-from-cc-to-ai-coding](https://github.com/ZhangHanDong/harness-engineering-from-cc-to-ai-coding) | 1.3K⭐，《马书》——逆向 Claude Code 源码学 Harness |
| [stablyai/orca](https://github.com/stablyai/orca) | 2.7K⭐，多 Agent 并行 IDE，理解 Agent 编排 |

### 实战级：自己造

| 方向 | 做法 |
|------|------|
| 写一个 Skill | 从你日常重复的工作中挑一个，写成 Skill |
| 写一个 CLI | 把 Skill 依赖的操作封装成命令行工具（参考 weread-cli） |
| 设计 Agent Loop | 画你的 Agent 的 Thought→Action→Observation 流程 |

---

## 学习节奏建议

```
Week 1-2：读完「第一层」所有文章 + 理解 Agent Loop
Week 3-4：写第一个 Skill（挑你最熟悉的场景）
Week 5-6：深入 Harness Engineering，读《马书》
Week 7-8：设计自己的 Agent 系统
```

---

## 速查表

### Agent 开发工具箱

| 工具 | 用途 |
|------|------|
| Claude Code | Agent CLI，支持 Skill、Hook、子 Agent |
| Codex | OpenAI 的 Agent CLI |
| Orca | 多 Agent 并行 IDE |
| MCP | 工具注册协议 |
| LangChain | Agent 框架（Python/JS） |

### 关键术语

| 术语 | = |
|------|-----|
| Agent Loop | Thought → Action → Observation |
| Skill | Agent 的可复用能力单元 |
| Tool | Agent 调用的外部功能 |
| MCP | 标准化工具注册协议 |
| Context Window | Agent 一次能"看到"的全部内容 |
| Harness | Agent 的外部脚手架 |
| Hook | 拦截 Agent Loop 的事件钩子 |

---

## 参见

- [[AI-Agent-核心概念对照]] — 八个核心概念一张表
- [[harness-engineering]] — Agent 脚手架六层架构
- [[claude-md-optimization]] — Context 注入文件优化
- [[cheat-on-content]] — 14 个 Skill 的实战拆解
- [[claude-code-mcp-browser]] — MCP 实战案例
