# AGENTS.md

本文件是 AI 编码代理的入口配置文件。不同 AI 工具可通过此文件找到对应的代理指令。

## 代理指令映射

- **Claude Code / Claude**: 参见 [CLAUDE.md](./CLAUDE.md)
- **Qoder (OpenCode)**: 参见 [.qoder/](./.qoder/)
- **Gemini CLI**: 参见 [GEMINI.md](./GEMINI.md)

## 项目理念

本项目基于 **Harness + Superpowers + OpenSpec** 三大理念构建：

- **Harness（工具集成层）**: 通过 .qoder/ 等目录，让项目配置在不同 AI 编码工具间可移植
- **Superpowers（超能力技能）**: 通过 skills/ 目录，为 AI 代理提供可复用的专业技能
- **OpenSpec（规范驱动开发）**: 通过 openspec/ 目录，实现 先定规范，再写代码的开发流程

## 快速开始

1. 阅读 [CLAUDE.md](./CLAUDE.md) 了解项目约定
2. 使用 /opsx:propose <你的想法> 创建变更提案
3. AI 代理会自动加载对应 skills/ 中的技能
