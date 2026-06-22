---
trigger: always_on
---
# Qoder 项目规则

## 项目架构

本项目基于 Harness + Superpowers + OpenSpec 三大理念构建。

### 技能系统 (Superpowers)
当用户请求涉及以下场景时，AI 应主动建议使用对应技能：
- 复杂需求分析 / 头脑风暴 -> skills/brainstorming/SKILL.md
- 大型功能开发 / 多任务 -> skills/subagent-driven-development/SKILL.md
- Bug 排查 -> skills/systematic-debugging/SKILL.md
- 编写计划 -> skills/writing-plans/SKILL.md
- 代码审查 -> skills/requesting-code-review/SKILL.md
- 并行开发 / Git Worktree -> skills/using-git-worktrees/SKILL.md

### 规范驱动开发 (OpenSpec)
使用 OpenSpec 工作流管理所有变更：
1. /opsx:propose - 创建变更提案
2. /opsx:apply - 实现变更
3. /opsx:archive - 归档变更
4. /opsx:explore - 纯调研、只读的思考阶段，不会生成任何规范文件、不会修改代码，核心是帮你在正式立项写需求前把思路理清楚

### 代码规范
- 遵循语言社区最佳实践
- 优先使用函数式编程风格
- 每个函数/方法必须有明确职责

### 文件组织
- src/ - 源代码
- tests/ - 测试文件
- docs/ - 项目文档
- openspec/ - 规范驱动开发工件
- skills/ - AI 代理技能定义
