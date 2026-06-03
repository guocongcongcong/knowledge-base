---
title: Claude Code Practical Tips (Boris @ Anthropic)
created: 2026-05-22
updated: 2026-05-22
type: concept
tags: [ai-tools, claude-code, prompting, workflow]
sources: [https://x.com/i/status/2057238154701426726]
confidence: high
contested: false
contradictions: []
---

# Claude Code 实用技巧 — Boris 演讲全解析

## 基本信息

| 项目 | 内容 |
|------|------|
| 演讲者 | Boris，Anthropic 技术团队成员，Claude Code 创建者 |
| 主题 | Claude Code 实用技巧与窍门 |
| 时长 | 27分52秒 |
| 来源 | Twitter @Etudecn 分享 |
| 热度 | 85万观看 / 1.5万喜欢 / 2719转帖 / 1.3万书签 |
| 转录 | raw/transcripts/claude-code-boris-talk.md |

## 核心要点

### 1. Claude Code 是什么
完全 agentic 的 AI 编码助手。不是行补全，而是构建功能、写整个函数/文件、修复 bug。兼容所有 IDE 和终端环境（本地/SSH/Tmux）。

### 2. 入门设置
- `terminal setup`：Shift+Enter 换行
- `theme`：暗色/亮色/Daltonized 主题
- `install GitHub app`：在 Issue/PR 中 @claude
- 自定义允许工具集（避免每次审批）
- macOS 语音听写输入提示词

### 3. 代码库 Q&A（新手最佳入口）
- 不问人，直接问 Claude 代码库相关问题
- Anthropic 新人技术入职从 **2-3周 → 2-3天**
- 无需索引、代码不上传、不训练
- 不是简单文本搜索：会深入分析类如何实例化、如何使用
- 可查 git 历史追溯代码演变（自动查 commit/issues）
- 每周站会："what did I ship this week" 自动总结

### 4. 编辑代码
- 小工具集：编辑文件、bash、搜索文件 — 自动组合
- **关键咒语**：`before you write code, make a plan`
- 不需要 plan mode，直接说就行
- 自动 commit → push → create branch → open PR

### 5. 反馈循环（最重要的技巧）
- 给 Claude 能检查自己工作的工具
- unit test / integration test / Puppeteer 截图 / iOS simulator
- 给 mock → 构建 UI → 截图对比 → 自动迭代优化
- **魔鬼在细节**：有反馈循环后，2-3 次迭代就能接近完美

### 6. CLAUDE.md 上下文体系
| 层级 | 位置 | 用途 |
|------|------|------|
| 项目 CLAUDE.md | repo 根目录 | 共享：bash 命令、MCP、架构、重要文件 |
| 本地 CLAUDE.md | repo 根（不提交） | 个人偏好 |
| 嵌套 CLAUDE.md | 子目录 | 按需自动加载 |
| 企业 CLAUDE.md | 企业根目录 | 全公司统一策略 |

保持简短！太长反而效果差。

### 7. 配置层级
项目 → 全局 → 企业策略（自动应用于全员）
- slash commands
- 权限：auto-approve / block 特定命令
- MCP JSON：提交到 repo 全员共享

### 8. 快捷键速查
| 快捷键 | 功能 |
|--------|------|
| Shift+Tab | 自动接受编辑模式 |
| # | 记忆（自动写入 CLAUDE.md） |
| ! | bash 模式（结果进入上下文） |
| Escape | 安全停止（不损坏会话） |
| Escape×2 | 跳回历史 |
| Ctrl+R | 查看完整输出 |
| resume / --continue | 恢复会话 |
| @文件 | 提及文件/文件夹入上下文 |

### 9. Claude Code SDK（-p 模式）
```bash
claude -p "prompt" --output-format json
```
- 支持 JSON / streaming JSON
- 可管道输入输出（gcp log → claude → 分析）
- 用于 CI、事件响应、自动化流水线
- 本质：「超智能 Unix 工具」
- Boris 原话："we barely scratched the surface"

### 10. 并行工作
- 多个终端 tab、多个 repo checkout
- SSH + Tmux 隧道
- Git Worktrees 隔离并行任务

## Q&A 精选

- **最难实现的功能**：bash 命令安全。区分只读/危险命令 + 静态分析 + 分层权限系统
- **多模态**：支持拖放/粘贴/文件路径引用图片（从 Day 1 就有，只是终端里难发现）
- **为什么是 CLI 不是 IDE**：终端是最大公约数；模型进步太快，IDE 可能年底就过时
- **内部使用率**：80% Anthropic 技术人员每天使用 Claude Code
- **ML 场景**：研究人员用 notebook 工具编辑和运行 notebooks

## 与 Hermes Agent 的关联

用户在 Hermes Agent 中大量使用 Claude Code（通过 claude-code skill）。本视频中的以下技巧直接适用：
- CLAUDE.md 上下文管理（已有但可优化）
- `-p` SDK 模式（用户经常用）
- 反馈循环（测试驱动开发）
- 快捷键（# 记忆功能）
- 并行多会话模式

## 观看建议

**强烈推荐观看**。如果你只用 Claude Code 的 20% 功能，这个视频帮你解锁剩下 80%。

## 相关页面

- [[Claude-Code-7个必装Skill]]
- raw/transcripts/claude-code-boris-talk.md
