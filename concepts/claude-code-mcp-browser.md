---
title: Claude Code MCP 浏览器联动
created: 2026-05-18
updated: 2026-05-18
type: concept
tags: [claude-code, mcp, browser, chrome, ai-tools]
sources:
  - https://www.douyin.com/video/7628833680907193627
confidence: medium
contested: false
contradictions: []
---

# Claude Code MCP 浏览器联动

## 是什么

通过 MCP (Model Context Protocol) 让 Claude Code 直接控制你**当前已登录的 Chrome 窗口**，保留登录态、Cookie 等信息，而不是打开一个新的无状态浏览器窗口。^[raw/transcripts/douyin-claude-code-mcp-browser.md]

## 核心价值

- **保留登录状态**：不需要每次重新登录网站
- **操作已登录页面**：可以直接在 GitHub、各类后台等已认证页面上执行操作
- **不需要额外浏览器插件**：通过 MCP 协议直连

## 配置步骤

### 1. 在 GitHub 打开对应仓库
找到 MCP browser 相关配置仓库

### 2. 复制配置命令
按页面提示复制配置命令

### 3. 命令行执行
在终端执行配置命令，注意添加 `--connect` 参数

### 4. 使用 Claude Code 操作浏览器
- 获取当前标签页信息
- 打开新标签页并抓取网页内容
- 在已登录页面执行自动化操作

## 适用场景

- 需要在已登录网站执行自动化操作
- 爬取需要认证的数据
- 跨页面工作流自动化
- 替代 Playwright 等需要独立浏览器的方案

## 兼容性

- Claude Code: 原生支持
- Codex: 评论区反馈应该也支持
- 通过 MCP 协议，理论上支持任意兼容 MCP 的 Agent

## 参见

- [[claude-code-mcp-browser]]
- [[Claude-Code-7个必装Skill]]
