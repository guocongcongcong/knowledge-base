---
title: AI Agent 核心概念对照
created: 2026-05-16
updated: 2026-05-16
type: comparison
tags: [ai-tools, claude-code, skills, memory, knowledge-base, obsidian]
sources: ["Hermes session 2026-05-16", "hermes-agent skill", "claude-code skill"]
confidence: medium
contested: false
contradictions: []
---

# AI Agent 核心概念对照

八个核心概念，解决同一个问题：**让 AI 记住该怎么做**。区别在颗粒度、持久性和作用范围。

## 概念速查

| 概念             | 本质    | 持久性 | 作用范围 | 类比        |
| -------------- | ----- | --- | ---- | --------- |
| Prompt         | 单次指令  | 一次性 | 当前对话 | 口头交代      |
| System Prompt  | 基础规则  | 永久  | 所有对话 | 员工手册      |
| Soul / Persona | 人格定义  | 会话级 | 当前会话 | 角色人设      |
| Memory         | 碎片信息  | 跨会话 | 所有对话 | 便利贴       |
| Skill          | 操作流程  | 跨会话 | 按需加载 | SOP 手册    |
| CLAUDE.md      | 项目上下文 | 跨会话 | 当前目录 | 项目 README |
| Tool           | 外部能力  | 永久  | 当前会话 | 工具箱       |
| MCP            | 通信协议  | 跨会话 | 全局   | USB 标准接口  |

## 逐条详解

### Prompt（提示词）
单次发给模型的指令。包含任务描述、约束、期望格式。对话结束即消失。

### System Prompt（系统提示词）
每轮对话自动注入的底层规则——你是谁、在哪台机器、能用什么工具、安全规则。用户看不见，不需要每次重复。

### Soul / Persona（人格）
System Prompt 的子集——专门管语气、性格、身份。Hermes 的 persona 文件定义 agent 怎么说话。改它就是改人设。

### Memory（记忆）
跨会话持久化的碎片信息条（100-300 字），每次对话自动注入。上限有字符限制（Hermes 默认 2,200 字）。

与 Skill 的关键区别：

| | Memory | Skill |
|------|--------|-------|
| 触发方式 | 每次都注入 | 任务匹配时才加载 |
| 内容 | 碎片信息 | 完整操作流程 |
| 长度 | 100-300 字 | 可数千字 |
| 例子 | "Docker 代理用 host.docker.internal" | "如何用 Claude Code 写小说" |

### Skill（技能）
可复用的操作流程手册。任务类型匹配时自动加载（不匹配不占 token）。与 [[Claude-Code-7个必装Skill]] 中讨论的 Claude Code Skill 是同一种概念。Hermes 的 skill 管理见 [[AI-Agent-核心概念对照]]（这是另一页待创建的概念）。

### CLAUDE.md / AGENTS.md（项目上下文）
项目根目录的上下文文件。Claude Code 进入该目录时自动加载。类似 Skill 但按目录触发而非按任务类型。适存项目技术栈、启停命令、目录结构。

### Tool（工具）
模型可调用的外部能力：`terminal`、`read_file`、`web_search`、`delegate_task`。不是文字，是动作。

### MCP（Model Context Protocol）
工具的标准接口协议。让任何 LLM 接任何外部服务。Hermes 和 Claude Code 都支持。

## 关系结构

```
System Prompt（最大外壳）
  ├── Soul / Persona（你是谁）
  ├── Memory 注入（碎片信息）
  ├── 工具列表（能做什么）
  └── 安全规则

Skill（按需加载的外挂模块）
  └── 引用 Tool 完成特定任务

CLAUDE.md（按目录加载）
  └── 类似 Skill 但绑定目录

MCP（工具通信协议）
  └── 连接 Tool 和外部服务
```

## 相关

- [[Claude-Code-7个必装Skill]] — Claude Code 的 Skill 生态实践
- [[家味协同项目概览]] — 项目 CLAUDE.md 的实际使用案例
