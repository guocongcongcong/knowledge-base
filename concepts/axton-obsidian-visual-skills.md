---
title: axton-obsidian-visual-skills — Obsidian 生图 Skill
created: 2026-05-13
updated: 2026-05-13
type: concept
tags: [ai-tools, claude-code, obsidian, visualization, skills]
sources: [douyin:赛博牛马, 2026-05-12]
confidence: medium
contested: false
contradictions: []
---

# axton-obsidian-visual-skills — Obsidian 生图 Skill

来源：抖音博主「赛博牛马」系列视频第 14 集，2026-05-12 发布。视频时长 2 分 21 秒，获 171 点赞、23 分享。

> 核心价值：将 Claude Code 与 Obsidian 连接，把文本想法直接转化为可编辑的可视化资产。

---

## GitHub 数据

| 指标 | 数值 |
|------|------|
| 仓库 | [axtonliu/axton-obsidian-visual-skills](https://github.com/axtonliu/axton-obsidian-visual-skills) |
| ⭐ Stars | **2,800** (2.8k) |
| 🍴 Forks | 249 |
| 📝 Commits | 19 |
| 🏷️ Tags | 3 |
| 📅 最后提交 | 2026 年 2 月（3 个月前） |
| 📜 协议 | 未注明 |

---

## 解决的问题

知识整理中的典型痛点：文字笔记写完了，但图表、架构图、知识地图总是"回头再补"——然后永远不补。

这个 Skill 让图表和笔记同步产生，是**文档、笔记和演示的生产力入口**。

---

## 三种可视化类型

| 类型 | 子目录 | 适用场景 | 特点 |
|------|--------|---------|------|
| **Excalidraw 图表生成器** | `excalidraw-diagram/` | 手绘风格图表 | 头脑风暴、示意图、非正式场景 |
| **Mermaid 可视化器** | `mermaid-visualizer/` | 工程文档、流程图 | 序列图、类图、流程图、技术文档 |
| **Obsidian Canvas 创建器** | `obsidian-canvas-creator/` | 知识地图 | 概念关联、项目全景、知识图谱 |

---

## 安装方式

1. 通过 Claude Code 的 Plugin Marketplace 安装（仓库内含 `.claude-plugin/marketplace.json`）
2. 手动安装：
   ```bash
   git clone https://github.com/axtonliu/axton-obsidian-visual-skills.git ~/.claude/skills/obsidian-visual-skills
   ```
3. 在 Obsidian 中安装对应的社区插件（Excalidraw、Mermaid 已内置）

---

## 使用流程

**先选载体 → 给结构 → 生成**：

- 手绘感 → 选 Excalidraw
- 工程文档 → 选 Mermaid
- 知识地图 → 选 Canvas

---

## 参见

- [[Claude-Code-7个必装Skill]] — Claude Code 7 个必装 Skill
- [[知识库压缩工具调研]] — 知识库工具对比
