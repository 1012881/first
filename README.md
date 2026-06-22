# my_first_project

基于 **Harness + Superpowers + OpenSpec** 理念构建的 AI 辅助编码项目。

## 三大核心理念

### 🔧 Harness — 工具集成层
让项目配置在不同 AI 编码工具间可移植。当前支持的集成层：
- .qoder/ — Qoder IDE 配置
- CLAUDE.md / AGENTS.md — Claude Code / 通用代理入口

### 🦸 Superpowers — 超能力技能
通过 skills/ 目录提供可复用的 AI 代理专业技能，包括：
- 子代理驱动开发 (SDD)
- 系统化调试
- 测试驱动开发 (TDD)
- 代码审查
- 可视化头脑风暴
- Git Worktree 并行开发
- 更多...

### 📋 OpenSpec — 规范驱动开发
" 先定规范，再写代码\。通过 openspec/ 目录管理变更提案、设计和任务。

## 快速开始

`ash
# 提出新功能
/opsx:propose 添加用户登录功能

# AI 代理会创建：
# openspec/changes/add-user-login/
# ├── proposal.md
# ├── design.md
# └── tasks.md

# 实现
/opsx:apply

# 完成后归档
/opsx:archive
`

## 目录结构

`
my_first_project/
├── .qoder/ # Harness: Qoder IDE 集成
├── AGENTS.md # 多工具代理入口
├── CLAUDE.md # 核心 AI 代理指令
├── openspec/ # OpenSpec: 规范驱动开发
│ ├── project.md
│ ├── specs/
│ ├── changes/
│ └── templates/
├── skills/ # Superpowers: 技能体系
├── docs/ # 项目文档
│ ├── plans/
│ └── specs/
├── hooks/ # Git/Session Hooks
├── src/ # 源代码
└── tests/ # 测试
`

## 参考资料

- [Superpowers](https://github.com/obra/superpowers) — AI 编码代理技能体系
- [OpenSpec](https://github.com/Fission-AI/OpenSpec) — 规范驱动开发框架
