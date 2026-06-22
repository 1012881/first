# CLAUDE.md

## 项目概述

本项目采用 **Harness + Superpowers + OpenSpec** 架构，专为 AI 辅助编码设计。

## 核心工作流

### 1. 规范驱动开发 (OpenSpec)

在编写任何代码之前，先通过 OpenSpec 流程对齐需求：

`
/opsx:propose <功能描述>    →  创建变更提案 (proposal.md, design.md, tasks.md)
/opsx:apply                 →  按 tasks.md 逐项实现
/opsx:archive               →  完成后归档到 openspec/changes/archive/
`

变更目录结构：
`
openspec/changes/<change-name>/
├── proposal.md          # 为什么要做、做什么
├── design.md            # 技术方案
├── tasks.md             # 实现任务清单
└── specs/               # 详细需求规范
`

### 2. 技能系统 (Superpowers)

skills/ 目录包含可复用的专业技能，AI 代理应根据任务自动选择合适的技能：

| 技能 | 用途 |
|------|------|
| brainstorming | 可视化头脑风暴，生成交互式 HTML 页面探索想法 |
| dispatching-parallel-agents | 将复杂任务拆分并分派给并行子代理 |
| executing-plans | 按照计划文档逐步执行实现 |
| finishing-a-development-branch | 完成开发分支的标准化流程 |
| receiving-code-review | 接收并处理代码审查反馈 |
| requesting-code-review | 发起代码审查请求 |
| subagent-driven-development | 子代理驱动的开发流程 (SDD) |
| systematic-debugging | 系统化调试方法 |
| test-driven-development | 测试驱动开发 |
| using-git-worktrees | 使用 Git Worktree 并行开发 |
| using-superpowers | 如何使用 Superpowers 技能体系 |
| verification-before-completion | 完成前验证检查清单 |
| writing-plans | 编写结构化的开发计划 |
| writing-skills | 编写新的技能定义 |

### 3. 工具集成层 (Harness)

.qoder/ 目录包含 Qoder IDE 的项目级配置，使技能和规则在不同工具间可移植。

## 项目约定

### 代码规范
- 遵循语言社区最佳实践
- 优先使用函数式编程风格（纯函数、不可变数据）
- 每个函数/方法必须有明确职责

### 文件组织
- src/: 源代码
- 	ests/: 测试文件（与 src 结构镜像）
- docs/plans/: 设计计划文档
- docs/specs/: 详细技术规范
- openspec/: 规范驱动开发工件（变更提案、设计、任务）

### Git 约定
- 使用 conventional commits: 	ype(scope): subject
- 分支命名: eature/<name>, ix/<name>, efactor/<name>

## 开发流程

1. **提出变更**: /opsx:propose 创建提案
2. **审查设计**: 检查 design.md 并确认方案
3. **实现**: AI 代理按 	asks.md 逐项执行
4. **审查代码**: 使用 equesting-code-review 技能
5. **验证**: 使用 erification-before-completion 技能
6. **归档**: /opsx:archive 归档变更

## 技能使用指南

当用户请求涉及以下场景时，应主动建议或使用对应技能：
- 复杂需求分析 → rainstorming
- 大型功能开发 → subagent-driven-development
- Bug 排查 → systematic-debugging
- 多任务并行 → dispatching-parallel-agents
- 分支完成 → inishing-a-development-branch
