---
title: 如何写出一个好的Skill
created: 2026-06-03
updated: 2026-06-03
type: concept
tags: [skills, ai-tools, claude-code, workflow]
sources: [https://v.douyin.com/GRb1iYMPmWE/]
confidence: medium
contested: false
contradictions: []
---

# 如何写出一个好的 Skill

> 来源：程序员Sunday 抖音视频「第9集 | 如何写出一个好的 skill（手把手详细教程）」2026-05-27
> 时长：19:41 | 👍 1870 · 💬 25 · ⭐ 2394 · ↗ 284

---

## 核心要点

### 1. Skill 的定义（00:32）

Skill 是一套**可复用的任务执行系统**。与 Prompt 的本质区别：

| | Skill | Prompt |
|---|---|---|
| 本质 | 任务执行系统 | 一次性指令 |
| 触发 | 有触发机制（关键词/场景匹配） | 手动输入 |
| 结构 | 有文件结构（SKILL.md + references/ + scripts/） | 纯文本 |
| 加载 | 按需加载（模型扫描匹配后自动激活） | 每次都全量注入 |
| 资源 | 分层资源（模板/脚本/参考文档） | 无 |
| 容错 | 脚本兜底（script 作为 fallback） | 无 |

**Skill 的五个核心要素：**
1. **触发机制** — 关键词/场景自动匹配
2. **文件结构** — SKILL.md 为主体，支持 references/、templates/、scripts/、assets/
3. **按需加载** — 模型按需扫描，不将所有 skill 全量注入上下文
4. **资源分层** — 模板、参考文档、脚本分离，各司其职
5. **脚本兜底** — 复杂操作用脚本实现，避免纯 LLM 推理出错

### 2. 定义 Skill 的注意事项（04:48）

- ✅ **给出具体的行动路径** — 不要只说"做什么"，要说"怎么做"（Step 1 → Step 2 → Step 3）
- ✅ **每个 Skill 只解决一类问题** — 单一职责，不要试图一个 skill 覆盖所有场景
- ✅ **命令要具体可执行** — 避免模糊指令，提供可直接复制运行的命令
- ✅ **记录常见坑点** — Pitfalls 是 skill 最有价值的部分之一
- ✅ **触发条件要精确** — 避免过度匹配或漏匹配

### 3. skill-creator 架构方案（09:37）

三位一体的架构设计：

- **第一层：元数据触发** — YAML frontmatter 定义 name/description/tags，由系统扫描匹配
- **第二层：内容执行** — Markdown body 定义操作步骤、命令、验证流程
- **第三层：脚本兜底** — scripts/ 目录下的可执行脚本，处理 LLM 不可靠的环节

```
skill-name/
├── SKILL.md          # 元数据 + 步骤（必须）
├── references/       # 参考文档（按需）
├── templates/        # 模板文件（按需）
├── scripts/          # 可执行脚本（兜底）
└── assets/           # 静态资源（按需）
```

### 4. 实战：编写 Skill（12:45）

实战流程：
1. 确定 skill 要解决的**单一问题**
2. 写好 **YAML frontmatter**（name/description/tags/触发条件）
3. 编写**操作步骤**，每步给出可执行命令
4. 添加 **Pitfalls**，记录已知坑点
5. 加入 **验证步骤**，确保 skill 执行后可检查结果

### 5. 验证 Skill（17:25）

验证清单：
- [ ] 触发条件是否正确匹配（不误触、不漏触）
- [ ] 操作步骤是否完整可执行（每一步都跑通）
- [ ] 命令是否在所有支持平台可用
- [ ] 坑点是否覆盖了已知失败场景
- [ ] 验证步骤是否能检测成功/失败

---

## 视频章节

| 时间 | 章节 |
|------|------|
| 00:00 | 引言 |
| 00:32 | skill 的定义（与 Prompt 的区别） |
| 04:48 | 定义 skill 的注意事项 |
| 09:37 | skill-creator 架构方案（三层设计） |
| 12:45 | 实战：手把手写一个 skill |
| 17:25 | 验证 skill 的方法 |

---

## 相关链接

- [[Claude-Code-7个必装Skill]] — Claude Code Skills 生态
- [[Hermes-Skill-Authoring]] — Hermes Agent skill 编写规范
- [[skill-creator]] — skill 创建工具
