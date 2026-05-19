---
title: CLAUDE.md 优化策略
created: 2026-05-18
updated: 2026-05-18
type: concept
tags: [claude-code, ai-tools, token-efficiency, context-engineering, skills]
sources:
  - https://www.douyin.com/video/7638645584525643018
  - https://www.douyin.com/video/7637164961961184550
confidence: medium
contested: false
contradictions: []
---

# CLAUDE.md 优化策略

## 核心理念

CLAUDE.md / AGENTS.md **不是文档，是 context 注入文件**。每行都会和代码、对话历史、工具输出一起塞进同一个 context window 抢注意力。越长 → 抢到的注意力越少 → Agent 越不听话。^[raw/transcripts/douyin-claude-md-too-long-agent-ignores.md]

## 长度红线

- **官方建议**：200 行以内
- **社区参考**：不超过 300 行
- **实操目标**：根文件压到 60 行以内（HumanLayer 的做法）
- 超过 200 行后越改越乱，再加东西只会让 Agent 越用越蠢 ^[raw/transcripts/douyin-claude-md-over-200-lines.md]

## 三步优化法 (Ali厂长)

### 第一步：根文件做薄
根 CLAUDE.md 只保留：
- 项目目标（一两句话）
- 协作原则（核心 2-3 条）
- 规则索引（指向 rules 目录的链接）

其余细则全部移出。

### 第二步：按关注点拆分
在 `.claude/rules/` 下按关注点建子文件：
```
.claude/rules/
├── code-style.md      # 代码风格
├── testing.md         # 测试规范
├── frontend.md        # 前端规则
├── backend.md         # 后端规则
├── security.md        # 安全规范
└── docs.md            # 文档规范
```

使用 `paths` frontmatter 做路径门禁，指定哪些规则对哪些文件生效。先搭结构，再用 `/memory` 实测。^[raw/transcripts/douyin-claude-md-over-200-lines.md]

### 第三步：用 /memory 命令逐条验证
确保每条规则：
- 真的被 Agent 读取并生效
- 不与其他规则冲突
- 文件大小可控

## 五个常见坑 (Ali厂长)

### 坑1：规则过多 → 规则被稀释
- 保持 200 行以内
- 每条加之前问"这条可以删吗？"
- 纯风格规则交给 linter/formatter 等工具，别写进 CLAUDE.md

### 坑2：只禁不导 → Agent 在解空间随机游走
- 每条"不要用 X"后面顺手补"推荐用 Y"
- 给 Agent 正向引导，而非只给禁区

### 坑3：@路径引用大段文档 → 全量加载
- 不要在 CLAUDE.md 里 @引用整个大文档
- 写清楚"什么时候去读哪个文件"的条件判断

### 坑4：命令不具体 → Agent 猜测错误
- 写清楚具体的单文件测试命令
- patch 命令、部署命令都要明确

### 坑5：临时状态永久化 → 过期事实
- 临时状态（如当前在修哪个 bug）放到独立的临时文件
- 按需加载，不要写在根 CLAUDE.md 里

## 自检方法

1. **Tinkleberry Test**：通过特定测试方法检查规则是否生效
2. **直接提问 Test**：向 Agent 提问验证它对规则的理解

## 本质认知

CLAUDE.md 和 AGENTS.md 是**软约束**，不能保证 Agent 一定遵守。真正的硬护栏要靠 **Hooks/Ceilings**（钩子系统）来实现。^[raw/transcripts/douyin-claude-md-too-long-agent-ignores.md]

## 参见

- [[Claude-Code-7个必装Skill]]
- [[harness-engineering]]
- [[claude-md-optimization]]
