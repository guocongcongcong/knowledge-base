---
title: Hermes Agent 三层路由架构设计
created: 2026-05-16
updated: 2026-05-16
type: concept
tags: [hermes, skills, routing, architecture, knowledge-base, memory]
sources: ["Hermes session 2026-05-16 实战复盘"]
confidence: high
contested: false
contradictions: []
---

# Hermes Agent 三层路由架构设计

## 问题起源

2026-05-16 一次实战中暴露的缺陷：

用户说「把这个记到知识库」→ Hermes 的 Memory 存了「知识库路径：~/Downloads/knowledge-base/」→ agent 知道往哪写，但**不知道要先加载 `knowledge-base` skill** → 写出的文件缺少 YAML frontmatter、没放对子目录、没更新 index.md 和 log.md → 格式全部不合格。

根因：**Memory 存了「是什么」（what），没存「要做什么」（what to do）。** 需要一个中间层把触发词翻译成动作。

## 三层架构

```
用户说 "记到知识库"
  │
  ▼
┌─────────────────────────────┐
│ 第一层：嗅探（SOUL.md）      │
│ 3行，强制注入，每次对话都读   │
│ "听到中文关键词 → 加载routing" │
└──────────┬──────────────────┘
           ▼
┌─────────────────────────────┐
│ 第二层：路由（routing skill） │
│ ~1.5KB，按需加载，不占Memory  │
│ "知识库" → knowledge-base    │
│ "续写"   → authors+claude    │
│ "内存"   → memory-management │
│ ...共20+条映射               │
└──────────┬──────────────────┘
           ▼
┌─────────────────────────────┐
│ 第三层：执行（各 skill）      │
│ 完整操作手册：步骤、命令、陷阱 │
│ knowledge-base / claude-code  │
│ memory-management / authors   │
└─────────────────────────────┘
```

### 各层职责

| 层 | 存什么 | 不存什么 | 改了什么影响什么 |
|-----|--------|---------|----------------|
| SOUL.md | "听到中文词→加载routing" | 不存具体映射 | 改这一行影响全局嗅觉灵敏度 |
| routing skill | 中文词→skill 映射表 | 不存操作步骤 | 改一行只影响一个触发词 |
| 各 skill | 完整操作流程 | 不依赖其他层 | 独立维护，改了 routing 不需要改 skill |

### 关键设计决策

**1. 为什么 SOUL.md 只放一行？**

因为 SOUL.md 是每次对话都强制注入的文本。如果放了 20 条映射规则，每次对话开头都重复这 20 条，稀释了真正重要的信息。一行嗅探规则 + 按需加载 routing = 零冗余。

**2. 为什么 routing 不用 Memory？**

Memory 上限 2,200 字符。20 条触发规则 × 50 字/条 = 1,000 字，一两条规则加进去还行，多了直接挤掉真正需要跨会话持久化的数据（API key 提示、项目路径、个人偏好）。routing 是流程数据，放 skill 正确。

**3. 为什么 routing 是 skill 而不是写死在 Persona 里？**

Persona 决定「你是谁」——这是用户可感知的人格。Routing 是「怎么做」——这是工具链。分开了，改人设不影响工作流，换工作流不影响人设。

**4. skill 会占用 Memory 配额吗？**

不会。Skill 是独立文件，按需加载（`skill_view(name)` 或自动匹配），不计入 2,200 字 memory 限制。routing skill 即使膨胀到 3KB 也不影响跨会话持久化数据的存储。

## 使用方式

### 安装

```bash
# 1. 创建 SOUL.md（如已有则追加内容）
echo '当用户使用中文关键词时，先加载 routing skill 查找对应操作流程。' > ~/.hermes/SOUL.md

# 2. 安装 routing 模板 skill
# 方法A：从 Hermes Skill Hub
hermes skills install routing-template

# 方法B：从 GitHub Gist 手动复制
mkdir -p ~/.hermes/skills/productivity/routing
curl -sL <raw-gist-url> -o ~/.hermes/skills/productivity/routing/SKILL.md
```

### 定制

打开 `~/.hermes/skills/productivity/routing/SKILL.md`，把表格里的示例项目名换成你自己的。例如：

```
-| 续写、写小说、接着写 | authors + claude-code | ...
+| 更新博客、写文章 | （你的写作 skill） | ...
```

### 维护

- 同一个中文关键词出现了 **≥2 次**，每次都触发同一个 skill → 加一行
- 偶尔一次的不加，保持表小而准
- 分不清该不该加的时候——不加

## 推广

- **GitHub Gist**：https://gist.github.com/guocongcongcong/5b9821dc92c05499878cf9bc59d3ff9f
- **Hermes Skill Hub**：搜索 `routing-template`
- **相关页面**：[[AI-Agent-核心概念对照]]、[[Claude-Code-6个隐藏能力]]
