---
title: Agent Loop工程手册（清华鑫哥）
created: 2026-06-10
updated: 2026-06-10
type: concept
tags: [ai-tools, agent-loop, loop-engineering, agent-architecture, 抖音笔记]
sources: [https://www.douyin.com/video/7649398299442564393]
confidence: medium
contested: false
contradictions: []
---

# Agent Loop 工程手册（清华鑫哥）

## 视频信息

- **来源**: 抖音 [清华鑫哥讲AI智能体](https://www.douyin.com/video/7649398299442564393)
- **作者**: 清华鑫哥（粉丝 18.3 万，获赞 33.7 万）
- **时长**: 9 分 16 秒
- **发布时间**: 2026-06-09
- **数据**: 1428 点赞 / 80 评论 / 1455 收藏 / 323 分享
- **标签**: #agentloop #loopengineering #智能体循环 #企业AI转型 #agentloop蓝皮书

## 核心观点

视频围绕一本 **Agent Loop 工程手册** 展开，回答一个核心问题：**Loop Engineering 硅谷爆火，是噱头还是下一波趋势？**

答案是：**不是噱头，是瓶颈转移的必然结果。** 现在的瓶颈不再是模型能力，而是"循环中的人"——通过 Agent Loop 设计，可以将人从循环中剥离出来，提高效率、降低成本。

## 视频章节要点

### 00:00 引言
Agent Loop 概念近期火爆，视频将系统性介绍 Agent Loop 工程手册的内容：构成、设计步骤、实战场景。

### 01:55 为什么是 Loop？
Agent Loop 爆发的根本原因是 **瓶颈转移**。过去的瓶颈在模型能力，现在的瓶颈在"循环中的人"。Loop Engineering 的目标是将人从 Agent 的执行循环中剥离出来，让 Agent 自主完成感知→思考→行动→观察的完整闭环。

### 02:23 Loop 的构成（五大构建 + Memory）
Agent Loop 包括 **五大构建 + 一个 Memory 记忆层**：

1. **Skills 技能层**：比 Prompt 更重要。每个 skill 是 Agent 的一项具体能力。
2. **Memory 记忆层**：跨循环的持久记忆，不是每次从头开始。
3. **Sub-agents 子代理层**：用于检查、评分、验证。子代理不是做任务的，是做质量控制的。
4. 其余两层（未具体展开，推测为 Planning 规划层和 Tool 工具层）

> 亮点：**Skills 比 Prompt 更重要**——这与 Hermes Agent 的设计哲学完全一致。

### 03:47 如何设计一个 Loop（5 步法）

1. **定义停止条件**：什么时候算完成？这是最容易被忽略、也是最重要的第一步。
2. **构建上下文**：Agent 需要知道什么才能开始工作？
3. **执行并捕获**：运行循环，捕获每一次工具调用和结果。
4. **反馈闭合循环**：将执行结果反馈回循环，让 Agent 判断"我完成了没有？还需要什么？"
5. **设置护栏**：硬边界——最大迭代次数、token 预算、不允许的操作。

### 05:16 Agent 编排的 6 种拓扑

6 种 Agent 编排拓扑，包括：
- 单 Agent 模式（有限制，会失败）
- 多 Agent 并行/串行模式
- （其余具体拓扑未展开）

关键约束：单 Agent 有明确的限制和失败模式，需要根据任务选择正确的拓扑。

### 06:15 实战场景及完整写法

7 个典型的实战场景，每个场景给出完整的 Loop 写法：
（视频中未逐条展开，推测涵盖代码生成、研究搜索、数据分析、内容创作、客服、自动化测试、企业流程等）

### 06:30 Loop 循环的真实成本

Loop 循环的成本较高——每次迭代都要重发完整历史，token 消耗 ×N。但可以通过优化策略节省 TOKEN 消耗量。具体优化方法未展开，但应与上下文压缩、滑动窗口、结构化记忆相关。

### 07:41 Loop Engineering 需要的技能

Loop Engineering 要求 **更高的系统设计能力**，不是简单调 API。未来工程师的角色将发生变化：
- 从"写代码"到"设计循环"
- 从"调试函数"到"调试 Agent 行为"
- 从"测试用例"到"护栏和边界条件"

### 08:18 从零开始的设计清单

5 步设计清单：
1. **任务分解**：把大任务拆成 Agent 能消化的粒度
2. **专家识别**：每个子任务需要什么"角色"（研究者、编码者、检查者）
3. **通信设计**：Agent 之间用什么格式传递信息（JSON/TOML/自然语言）
4. **契约治理**：定义输入输出合约，防止 Agent 跑偏
5. **检查表**：每次循环结束后的验证清单

### 08:28 工具素材
视频提到配套有工具素材和手册（可能是付费/关注获取）。

## 关键评论观点

- **渔不鱼**: "要想设计 loop，你要有可量化的指标，问题是很多需求没办法量化的。这个最早好像来自 karpathy 开发的 auto research，用来做模型自主训练的。"
- **小钦童鞋**: "应该类似于 Claude Code dynamic workflows 概念，规定工作流路径与循环，每个节点用多个 subagent 并行或串行，来做上下文隔离。"
- **天天小萌懵**: "听完了感觉这个 loop 更偏向软件开发人员吧，对于其他行业比如零售或者服务业，我想不出该怎么结合。"
  - 作者回复: **"Agent 能用在哪儿，loop 就能用在哪儿"**
- **黄小小**: "Token 卖不动了。一个 agent 花费不够，让 10 个 agent 一起干活，花费 10 倍。模型公司爽歪歪。"
- **司庭花**: "跟 Harness Engineering 有什么区别？在于提出了具体的方法论？"
- **AI时代入局**: "我设定个 /goal，剩下的就是 codex 自动寻找路径去实现目标了，和这个 loop 有什么区别没。"

## 与现有知识的整合

### 与 Agent Loop Engineering 概念页的关系

清华鑫哥的框架与社区总结的五大模式高度吻合：

| 鑫哥的框架 | 社区对应概念 |
|-----------|-------------|
| 5 步设计法 | ReAct + Plan-Execute 的工程化落地 |
| Sub-agents 检查层 | Multi-Agent Collaboration 的质量控制模式 |
| 护栏（停止条件 + 硬边界） | Anthropic 的 "不要过度自主" 原则 |
| Skills > Prompt | Hermes Agent 的 Skill 自进化系统 |
| 6 种拓扑 | LangGraph 的 DAG 编排 / Multi-Agent 协作 |

### 与 Harness Engineering 的区别

司庭花的评论区提问很关键。两者的区别：
- **Harness Engineering**：Agent 的外部脚手架——工具、权限、记忆、人机交互接口
- **Loop Engineering**：Agent 的内部运行逻辑——感知→思考→行动→观察的循环设计

一个是"给 Agent 配什么装备"，一个是"Agent 怎么运转"。

### 争议点

视频评论区暴露了 Loop Engineering 的核心争议：
1. **量化困难**: 很多需求无法量化评估，"完成"的定义模糊——这是 Agent Loop 最根本的工程挑战。
2. **Token 经济质疑**: 多 Agent Loop 放大了 token 消耗，是否真的值？
3. **适用边界**: 是开发者的专属工具，还是普适的企业级模式？

## 相关概念

- [[agent-loop-engineering]] — Agent Loop 工程全景：5 大模式 + 4 大框架对比
- [[harness-engineering]] — Harness Engineering 六层架构
- [[last30days-skill]] — Agent Loop 在多源搜索中的具体应用
- [[Hermes-Agent-三层路由架构设计]] — Hermes 的元认知循环
- [[deer-flow-multi-agent]] — 多 Agent 协作循环
