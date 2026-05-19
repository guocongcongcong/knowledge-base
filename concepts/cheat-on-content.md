---
title: cheat-on-content — 内容创作 AI 校准系统
created: 2026-05-18
updated: 2026-05-18
type: concept
tags: [ai-tools, content-creation, claude-code, skills, analytics, growth]
sources:
  - https://github.com/XBuilderLAB/cheat-on-content
confidence: medium
contested: false
contradictions: []
---

# cheat-on-content — 内容创作 AI 校准系统

## 是什么

一套 Claude Code / Codex 的 **14 个子 Skill 集合**，把内容创作从赌博变成校准实验。

- GitHub: https://github.com/XBuilderLAB/cheat-on-content
- Stars: 2,300+
- 安装: `git clone` → `bash install.sh`
- 支持: Claude Code (默认) / Codex (`--codex`) / 双装 (`--all`)

## 核心闭环

```
📊 Score → 🎯 Blind-predict → 🚀 Publish → 📈 T+3d Retro → 🧬 Evolve Rubric
```

每一步都被日志记录，3 天后对比预测 vs 实际，公式自动进化。

## 日常命令

```bash
score this scripts/<...>.md       # 仅评分
start prediction scripts/<...>.md # 盲预测 + 决策日志
shot scripts/<...>.md             # 创建视频文件夹
shipped https://...               # 标记已发布
retro videos/<...>/               # T+3d 复盘
status / fetch trends / find topic / bump rubric / find benchmark
```

## 与通用 AI 的本质区别

| 通用 AI | cheat-on-content |
|---------|-----------------|
| 告诉所有人一样的东西 | 只服务你一个账号 |
| 不记得你 | 每次发布更新对你的理解 |
| 全局平均评分 | 从你的历史反推公式 |
| 3 个月后判断力不变 | 3 个月后精度是第 1 天的 10 倍 |

## 技术亮点

- **盲预测机制**：预测时隔离历史实际数据，防止自我欺骗
- **跨模型审计**：升级公式需独立模型验证
- **Rubric 是工作台不是博物馆**：被数据推翻的观察自动删除
- **平台适配器**：支持抖音等平台数据接入
- **Hook 感知**：支持 Hook 的 Agent 在每次 session 开始时自动报告 buffer + 待复盘内容

## 安装

```bash
git clone https://github.com/XBuilderLAB/cheat-on-content.git
cd cheat-on-content
bash install.sh          # Claude Code
bash install.sh --codex  # Codex
bash install.sh --all    # 两个都装
```

在内容项目目录中，对 Agent 说 `初始化 cheat-on-content`，回答 5 个 yes/no 问题完成引导。建议导入 5-10 个对标账号样本作为锚点。

## 升级注意

v1.3 → v1.4 有破坏性迁移：盲通道完整性修复，需运行 `/cheat-migrate`。

## 参见

- [[claude-md-optimization]] — CLAUDE.md 优化策略
- [[Claude-Code-7个必装Skill]] — Claude Code Skill 生态
