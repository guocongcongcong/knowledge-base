---
title: Claude Code 6个隐藏能力
created: 2026-05-16
updated: 2026-05-16
type: concept
tags: [claude-code, ai-tools, skills]
sources: ["抖音@阿森编程日记 2026-05-14"]
confidence: high
contested: false
contradictions: []
---

# Claude Code 6个隐藏能力

> 来源：抖音 @阿森编程日记，2026-05-14 发布
> 核心理念：别只把 Claude Code 当聊天写代码工具，掌握这些能力把它从临时助手升级为稳定开发工作流。

## 六大能力

### 1. 项目记忆 — `/init`
让 Claude Code 生成 `CLAUDE.md` 项目说明文件，先认识项目再开始干活。

相关：[[AI-Agent-核心概念对照]] 中的 CLAUDE.md 概念。

### 2. Plan Mode
先读项目、拆方案、判断风险，再进入执行。避免盲目开工。

### 3. 上下文压缩 — `/compact`
压缩对话上下文，保留重要信息，防止 token 超限。

### 4. 自定义命令 — Custom Slash Commands
将常用提示词沉淀成自定义命令（`.claude/commands/` 目录），随时复用。

### 5. Sub Agent — 子代理
分工合作。主对话统筹方向，子 agent 分别负责审查、排错、测试和文档。

相关：[[Claude-Code-7个必装Skill]] 中的 subagent 实践。

### 6. Hooks — 自动质检
理解成自动质检员。在特定事件触发时自动执行操作——比如写代码后自动运行 lint、提交前检查格式。

在 `settings.json` 中配置，支持的事件类型见 [[AI-Agent-核心概念对照]] 中的 Tool 和 MCP 关系说明。

## 与 Hermes Agent 的概念对照

| Claude Code | Hermes Agent |
|-------------|-------------|
| `/init` → CLAUDE.md | 项目 CLAUDE.md（自动加载） |
| Plan Mode | Skill 中的 writing-plans |
| `/compact` | 自动上下文压缩 |
| Custom Commands | Skill（按需加载） |
| Sub Agent | delegate_task / terminal+claude -p |
| Hooks | Cron / Webhook / Curator |
