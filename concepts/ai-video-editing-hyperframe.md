---
title: AI 视频剪辑（Hyperframe）
created: 2026-05-18
updated: 2026-05-18
type: concept
tags: [ai-tools, video-editing, hyperframe, automation, claude-code]
sources:
  - https://www.douyin.com/video/7631191369612135680
confidence: medium
contested: false
contradictions: []
---

# AI 视频剪辑（Hyperframe）

用 AI 编程智能体 + Hyperframe 开源项目实现全自动视频剪辑，完全不需要碰剪辑软件。^[raw/transcripts/douyin-ai-video-editing-hyperframe.md]

## 技术栈

- **核心工具**：Hyperframe 开源项目
- **驱动引擎**：任意编程智能体（Claude Code / Codex）
- **输出**：自动添加大字、字幕与转场效果

## 工作流程

### 基础流程
1. **喂素材**：上传原始视频/图片素材
2. **传带时间戳字幕**：提供 SRT 或带时间戳的字幕文件
3. **自然语言微调**：用自然语言描述想要的剪辑效果
4. **AI 自动生成**：智能体调用 Hyperframe 完成剪辑

### 进阶玩法
- 把整个工作流沉淀为可复用的 **Skill**
- 下次直接一键成片，输入素材 → 输出成品

## 迭代过程（本视频案例）

1. 第一版效果 → 不满意
2. 迭代 → 第二版效果
3. 继续优化 → 最终版
4. 总结流程和优缺点

## 注意事项

- **Windows 警告**：在 Windows 上使用 Codex APP 执行此流程会导致 token usage 爆表且无法完成任务
- 建议在 Mac/Linux 环境下使用 Claude Code

## 适用场景

- 短视频批量制作
- 字幕自动叠加
- 固定格式的视频模板化生产
- 自媒体日更工作流

## 参见

- [[Claude-Code-7个必装Skill]]
- [[cheat-on-content]]
