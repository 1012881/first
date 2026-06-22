# OpenSpec + Superpowers 使用指南

> 本文档介绍 OpenSpec（规范驱动开发）和 Superpowers（AI 代理技能框架）在 my_first_project 中的安装结果和使用方法。

---

## 目录

1. [环境概览](#环境概览)
2. [OpenSpec — 规范驱动开发](#openspec--规范驱动开发)
   - [核心概念](#核心概念)
   - [斜杠命令](#斜杠命令)
   - [完整工作流示例](#完整工作流示例)
   - [CLI 命令参考](#cli-命令参考)
3. [Superpowers — AI 代理技能体系](#superpowers--ai-代理技能体系)
   - [核心概念](#核心概念-1)
   - [技能列表](#技能列表)
   - [标准开发流程](#标准开发流程)
   - [如何触发技能](#如何触发技能)
4. [两者协作](#两者协作)
5. [项目目录结构](#项目目录结构)
6. [常见问题](#常见问题)

---

## 环境概览

| 组件 | 版本/状态 | 安装方式 |
|------|----------|---------|
| **OpenSpec CLI** | v1.4.1 | `npm install -g @fission-ai/openspec@latest` |
| **OpenSpec 配置** | 已初始化 | `openspec init`（Qoder 集成） |
| **Superpowers Skills** | v1.x（完整版） | 从 GitHub 仓库同步 |
| **Node.js** | ≥20.19.0 | 系统环境 |

---

## OpenSpec — 规范驱动开发

OpenSpec 是一个轻量级的**规范驱动开发（SDD）**框架，让人类和 AI 在写任何代码之前先对齐"要构建什么"。

### 核心理念

```
→ 灵活而非僵化（fluid not rigid）
→ 迭代式而非瀑布式（iterative not waterfall）
→ 简单而非复杂（easy not complex）
→ 为棕地项目而建，不限于绿地项目
```

### 核心概念

- **Change（变更）**：每个功能/修复都是一个变更，拥有独立目录
- **Artifact（工件）**：每个变更包含以下工件：
  - `proposal.md` — 变更的原因和目标
  - `design.md` — 技术方案
  - `tasks.md` — 实施任务清单
  - `specs/` — 需求规格说明

### 斜杠命令

在 Qoder 对话中直接使用以下命令：

| 命令 | 说明 | 示例 |
|------|------|------|
| `/opsx:propose` | 创建新变更并生成所有工件 | `/opsx:propose add-dark-mode` |
| `/opsx:apply` | 按任务清单逐步实现变更 | `/opsx:apply add-dark-mode` |
| `/opsx:archive` | 归档已完成的变更 | `/opsx:archive add-dark-mode` |
| `/opsx:explore` | 探索已有规范和变更 | `/opsx:explore` |
| `/opsx:sync` | 同步 delta spec 到主规范 | `/opsx:sync` |

### 完整工作流示例

#### 第一步：提出变更（Propose）

```
用户: /opsx:propose add-user-login

AI: 创建 openspec/changes/add-user-login/
  ✓ proposal.md — 为什么做，要改变什么
  ✓ specs/ — 需求和场景
  ✓ design.md — 技术方案
  ✓ tasks.md — 实施检查清单
  准备就绪！
```

#### 第二步：实施变更（Apply）

```
用户: /opsx:apply

AI: 正在实施任务...
  ✓ 1.1 创建登录页面组件
  ✓ 1.2 添加表单验证逻辑
  ✓ 2.1 集成 API 认证接口
  ✓ 2.2 处理登录状态管理
  所有任务完成！
```

#### 第三步：归档（Archive）

```
用户: /opsx:archive

AI: 归档到 openspec/changes/archive/2025-06-21-add-user-login/
  规范已更新。准备下一个功能。
```

### CLI 命令参考

除了在对话中使用斜杠命令，也可以在终端直接使用 CLI：

```bash
# 查看帮助
openspec --help

# 查看版本
openspec --version

# 初始化项目（已完成）
openspec init

# 更新 OpenSpec 配置
openspec update

# 创建新变更
openspec new change "my-change-name"

# 查看变更状态
openspec status --change "my-change-name"

# 查看变更状态（JSON 格式）
openspec status --change "my-change-name" --json

# 列出所有变更
openspec list

# 获取工件创建指令
openspec instructions proposal --change "my-change-name" --json

# 全局升级
npm install -g @fission-ai/openspec@latest
```

---

## Superpowers — AI 代理技能体系

Superpowers 是一套完整的 AI 编码代理**技能框架和开发方法论**，由一组可组合的技能和初始指令组成，确保 AI 代理遵循最佳实践。

### 核心理念

- **测试驱动开发（TDD）**——先写测试，永远如此
- **系统化优先于临时方案**——用流程替代猜测
- **降低复杂度**——简单性是首要目标
- **证据优先于声明**——验证后再宣称成功

### 技能列表

#### 规划类

| 技能 | 触发条件 | 说明 |
|------|---------|------|
| **brainstorming** | 编写代码前 | 通过提问精炼想法，探索替代方案，生成可视化设计文档 |
| **writing-plans** | 设计获批后 | 将工作拆分为 2-5 分钟的小任务，含精确文件路径和验证步骤 |
| **using-git-worktrees** | 设计获批后 | 创建隔离的 Git Worktree 工作空间，在新分支上进行开发 |

#### 实现类

| 技能 | 触发条件 | 说明 |
|------|---------|------|
| **test-driven-development** | 实现任何功能/修复前 | RED-GREEN-REFACTOR 循环：写失败测试→最小代码→重构 |
| **subagent-driven-development** | 有计划时 | 为每个任务派发独立子代理，含两阶段审查（规范合规 + 代码质量） |
| **executing-plans** | 有计划时 | 批量执行任务，含人工检查点 |
| **dispatching-parallel-agents** | 需并行处理时 | 并行调度多个子代理工作流 |

#### 质量类

| 技能 | 触发条件 | 说明 |
|------|---------|------|
| **requesting-code-review** | 任务间 | 按计划审查代码，按严重程度报告问题 |
| **receiving-code-review** | 收到审查反馈 | 结构化地响应和处理审查意见 |
| **verification-before-completion** | 任务完成时 | 确保修复真正生效后再宣称完成 |

#### 调试类

| 技能 | 触发条件 | 说明 |
|------|---------|------|
| **systematic-debugging** | 遇到 Bug/测试失败 | 4 阶段根因分析：复现→模式分析→假设验证→实施修复 |

#### 管理类

| 技能 | 触发条件 | 说明 |
|------|---------|------|
| **finishing-a-development-branch** | 任务全部完成 | 验证测试，提供合并/PR/保留/丢弃选项，清理 Worktree |

#### 元技能

| 技能 | 触发条件 | 说明 |
|------|---------|------|
| **using-superpowers** | 首次使用 | 技能系统入门介绍 |
| **writing-skills** | 创建新技能 | 按最佳实践编写新的技能定义 |

### 标准开发流程

Superpowers 定义了标准的端到端开发流程：

```
1. brainstorming           → 精炼需求，生成设计文档
2. using-git-worktrees      → 创建隔离开发分支
3. writing-plans            → 拆分为 2-5 分钟的小任务
4. subagent-driven-development   → 子代理逐个执行任务
   或 executing-plans       → 批量执行（含检查点）
5. test-driven-development  → 每个任务 RED-GREEN-REFACTOR
6. requesting-code-review   → 任务间代码审查
7. finishing-a-development-branch → 完成、合并、清理
```

### 如何触发技能

**方式一：对话中自然触发**

AI 代理会根据当前上下文自动判断应使用的技能。例如：
- 提到 Bug → 自动触发 `systematic-debugging`
- 开始写代码 → 自动触发 `test-driven-development`
- 需求讨论 → 自动触发 `brainstorming`

**方式二：明确请求**

```
用户: 使用 brainstorming 技能讨论用户认证方案
用户: 用 subagent-driven-development 实现这个功能
用户: 使用 systematic-debugging 排查登录失败问题
```

**方式三：启动时自动加载**

`hooks/session-start` 在每次 AI 会话启动时自动运行，加载 Superpowers 核心上下文。

---

## 两者协作

OpenSpec 和 Superpowers 是互补的工具：

| 维度 | OpenSpec | Superpowers |
|------|----------|-------------|
| **关注点** | 规范管理（What） | 实施方法论（How） |
| **产出** | proposal / design / tasks / specs | TDD 循环 / 代码审查 / 调试流程 |
| **工作流** | Propose → Apply → Archive | 规划 → 实现 → 审查 → 完成 |

### 典型协作流程

```
┌─────────────────────────────────────────┐
│  用户: "我想添加深色模式"                │
└─────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────┐
│  OpenSpec: /opsx:propose add-dark-mode  │
│  → 创建 proposal / design / tasks       │
│  (Superpowers brainstorming 辅助讨论)    │
└─────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────┐
│  OpenSpec: /opsx:apply                  │
│  → 按 tasks.md 逐步实现                 │
│    (Superpowers TDD 驱动每个任务)        │
│    (Superpowers code-review 审查质量)    │
└─────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────┐
│  OpenSpec: /opsx:archive                │
│  → 归档变更，更新规范                    │
│  (Superpowers finishing-branch 清理)     │
└─────────────────────────────────────────┘
```

---

## 项目目录结构

安装完成后，项目关键目录结构如下：

```
my_first_project/
├── .qoder/                          # Qoder IDE 集成（OpenSpec 生成）
│   ├── commands/opsx/               # 斜杠命令定义
│   │   ├── propose.md               #   /opsx:propose
│   │   ├── apply.md                 #   /opsx:apply
│   │   ├── archive.md               #   /opsx:archive
│   │   ├── explore.md               #   /opsx:explore
│   │   └── sync.md                  #   /opsx:sync
│   ├── skills/openspec-*/           # OpenSpec 技能定义
│   ├── context/                     # 项目上下文
│   └── rules/                       # 项目规则
│
├── openspec/                        # OpenSpec 规范目录
│   ├── config.yaml                  # OpenSpec 配置（上下文 + 工具集成）
│   ├── changes/                     # 活跃变更
│   │   └── add-todo-page/           #   示例变更
│   │       ├── proposal.md
│   │       ├── design.md
│   │       └── tasks.md
│   ├── specs/                       # 主规范文件
│   └── templates/                   # 工件模板
│       ├── proposal-template.md
│       ├── design-template.md
│       └── tasks-template.md
│
├── skills/                          # Superpowers 技能库
│   ├── brainstorming/               #   头脑风暴（含可视化脚本）
│   ├── dispatching-parallel-agents/ #   并行代理调度
│   ├── executing-plans/             #   执行计划
│   ├── finishing-a-development-branch/ # 完成开发分支
│   ├── receiving-code-review/       #   接收代码审查
│   ├── requesting-code-review/      #   请求代码审查
│   ├── subagent-driven-development/ #   子代理驱动开发（含脚本）
│   ├── systematic-debugging/        #   系统化调试（含参考文档）
│   ├── test-driven-development/     #   测试驱动开发（含反模式参考）
│   ├── using-git-worktrees/         #   Git Worktree
│   ├── using-superpowers/           #   使用指南（含工具参考）
│   ├── verification-before-completion/ # 完成前验证
│   ├── writing-plans/               #   编写计划
│   └── writing-skills/              #   编写技能（含最佳实践）
│
├── hooks/                           # 会话钩子
│   ├── session-start                #   会话启动脚本
│   ├── hooks.json                   #   钩子配置
│   └── hooks-cursor.json            #   Cursor 专用钩子配置
│
├── src/                             # 源代码
├── tests/                           # 测试文件
└── docs/                            # 文档
    └── OpenSpec-Superpowers-使用指南.md  # ← 本文档
```

---

## 常见问题

### Q: 如何升级 OpenSpec？

```bash
# 升级全局 CLI
npm install -g @fission-ai/openspec@latest

# 更新项目配置
cd my_first_project
openspec update
```

### Q: 如何升级 Superpowers？

Superpowers 通过 GitHub 仓库分发。更新步骤：

```bash
# 克隆最新版本到临时目录
git clone https://github.com/obra/superpowers.git superpowers_temp --depth 1

# 同步 skills 和 hooks
Copy-Item -Path "superpowers_temp/skills/*" -Destination "my_first_project/skills/" -Recurse -Force
Copy-Item -Path "superpowers_temp/hooks/*" -Destination "my_first_project/hooks/" -Recurse -Force

# 清理
Remove-Item -Path "superpowers_temp" -Recurse -Force
```

### Q: 如何创建新的 OpenSpec 变更？

在 Qoder 对话中直接使用：
```
/opsx:propose <变更名称>
```

例如：`/opsx:propose add-search-function`

### Q: TDD 太耗时怎么办？

Superpowers 的 TDD 技能强调：**写测试比调试快**。TDD 在实践中通常：
- 首次修复率：95% vs 40%（非 TDD）
- 引入新 Bug：接近零 vs 常见
- 总体耗时：更少（减少调试时间）

### Q: 斜杠命令不工作？

1. 确认已运行 `openspec init`
2. 重启 IDE 使斜杠命令生效
3. 检查 `.qoder/commands/opsx/` 目录下是否有命令文件

### Q: 如何禁用遥测？

```bash
# OpenSpec 遥测退出
export OPENSPEC_TELEMETRY=0

# Superpowers 遥测退出
export SUPERPOWERS_DISABLE_TELEMETRY=true
```

---

## 参考链接

- OpenSpec GitHub: [https://github.com/Fission-AI/OpenSpec](https://github.com/Fission-AI/OpenSpec)
- Superpowers GitHub: [https://github.com/obra/superpowers](https://github.com/obra/superpowers)
- OpenSpec 文档: [https://github.com/Fission-AI/OpenSpec#docs](https://github.com/Fission-AI/OpenSpec#docs)
- Superpowers Discord: 见 Superpowers README
