---
title: Claude Code 7个必装Skill
created: 2026-05-13
updated: 2026-05-13
type: concept
tags: [ai-tools, claude-code, skills, programming]
sources: [douyin:阿森编程日记（AI自动化）, 2026-05-11]
confidence: medium
contested: false
contradictions: []
---

# Claude Code 7个必装Skill

来源：抖音博主「阿森编程日记（AI自动化）」2026-05-11 发布。视频时长 1 分 55 秒，获 2.1 万点赞、188 评论、2613 分享。

> 核心观点：大部分人只用到了 Claude Code 30% 的能力，装了这 7 个 Skill 才能真正发挥全部能力。

---

## GitHub 数据总览

| # | Skill | 仓库 | ⭐ Stars | 类型 |
|---|-------|------|----------|------|
| 1 | Superpowers | [obra/superpowers](https://github.com/obra/superpowers) | **188,994** | 独立仓库 |
| 2 | PDF | Claude Code 内置 | — | 内置 |
| 3 | humanizer-zh | [op7418/Humanizer-zh](https://github.com/op7418/Humanizer-zh) | **7,466** | 独立仓库 |
| 4 | planning-with-files | [OthmanAdi/planning-with-files](https://github.com/OthmanAdi/planning-with-files) | **21,117** | 独立仓库 |
| 5 | frontend-design | [Ilm-Alan/frontend-design](https://github.com/Ilm-Alan/frontend-design) | **29** | 独立仓库 |
| 6 | Skill review | Claude Code 内置 | — | 内置 |
| 7 | skill-creator | Claude Code 内置 + [FrancyJGLisboa/agent-skill-creator](https://github.com/FrancyJGLisboa/agent-skill-creator) | **915** | 内置+社区 |

**补充数据：**
- Claude Code 主仓库 [anthropics/claude-code](https://github.com/anthropics/claude-code) ⭐**123,000**
- Superpowers 中文版 [jnMetaCode/superpowers-zh](https://github.com/jnMetaCode/superpowers-zh) ⭐**2,772**

---

## 7 个 Skill 详解

### 1. Superpowers — 全能 Skill ⭐188,994

`obra/superpowers` | Agentic skills framework & software development methodology

覆盖开发全流程，帮助程序员梳理需求、拆分任务、系统化调试。

- **定位**：总控型 Skill，相当于 Claude Code 的 "操作系统"
- **功能**：需求梳理 → 任务拆分 → 系统调试，全链路覆盖
- **生态**：社区可编辑 skills 库 [obra/superpowers-skills](https://github.com/obra/superpowers-skills) ⭐656，实验性 lab [obra/superpowers-lab](https://github.com/obra/superpowers-lab)
- **中文版**：[jnMetaCode/superpowers-zh](https://github.com/jnMetaCode/superpowers-zh) ⭐2,772，完整汉化 + 6 个中国原创 skill，支持 Claude Code/Copilot CLI/Hermes/Cursor 等 16 款工具

### 2. PDF — 文档处理神器（内置）

Claude Code 内置 skill。支持读取、合并、拆分 PDF，还支持 OCR 扫描件识别。

- **功能**：PDF 读取 / 合并 / 拆分 + OCR 识别
- **适用场景**：阅读文档、处理扫描件、批量文档操作
- **备注**：无独立高星 GitHub 仓库（社区有多个 fork 但均 <10 stars），属于 Claude Code 官方内置能力

### 3. humanizer-zh — 去 AI 味神器 ⭐7,466

`op7418/Humanizer-zh` | Humanizer 汉化版

将生硬表达换成接地气的人话，减少模板味。

- **功能**：把 AI 腔调的文本改写为自然中文
- **适用场景**：写文章、文案、邮件，避免 "模板味"
- **数据**：7,466 stars，Fork 较多

### 4. planning-with-files — 大项目救星 ⭐21,117

`OthmanAdi/planning-with-files` | Manus 风格持久化 Markdown 规划

持久化项目规划，跨会话不丢进度，适合碎片化时间开发。

- **功能**：将项目计划写入文件，跨 session 保持进度
- **适用场景**：大项目分段开发、碎片化时间工作
- **数据**：21,117 stars，多个 fork（含中文版）

### 5. frontend-design — 前端颜值救星 ⭐29

`Ilm-Alan/frontend-design` | 8 种美学锚点

让 Claude Code 写的前端更专业，后端程序员也能做出好看规范。

- **功能**：8 种美学锚点（palette/typography/texture → CSS tokens），选一个即可
- **适用场景**：后端程序员做前端、快速出原型
- **数据**：29 stars（社区热度较低，但设计理念扎实）

### 6. Skill review — 代码质量守护神（内置）

Claude Code 内置 skill。并行审查代码，找 bug、查安全漏洞、优化代码规范，减少代码出错率。

- **功能**：并行代码审查，自动检查 bug / 安全漏洞 / 规范
- **适用场景**：代码提交流程中的质量把关
- **备注**：属于 Claude Code 内置审查能力（社区版 [decebals/skill-review](https://github.com/decebals/skill-review) ⭐2）

### 7. skill-creator — 压轴神器 ⭐915（社区版）

Claude Code 内置 + [FrancyJGLisboa/agent-skill-creator](https://github.com/FrancyJGLisboa/agent-skill-creator) ⭐915

让你自己定制 Skill，让 AI 适配你的需求。

- **功能**：创建自定义 Skill，满足个性化工作流
- **社区版**：支持 14+ 工具（Claude Code/Copilot/Cursor/Windsurf/Codex/Gemini/Kiro 等）
- **数据**：915 stars（社区版），官方版内置于 anthropics/claude-code

---

## 安装方式

大部分 skill 通过 Claude Code Plugin Marketplace 安装：
```
/claude install skill-name
```

独立仓库手动安装：
```bash
# Superpowers
git clone https://github.com/obra/superpowers.git ~/.claude/skills/superpowers

# humanizer-zh
git clone https://github.com/op7418/Humanizer-zh.git ~/.claude/skills/humanizer-zh

# planning-with-files
git clone https://github.com/OthmanAdi/planning-with-files.git ~/.claude/skills/planning-with-files
```

---

## 参见

- [[axton-obsidian-visual-skills]] — Obsidian 可视化 Skill
- [[知识库压缩工具调研]] — 知识库工具对比
