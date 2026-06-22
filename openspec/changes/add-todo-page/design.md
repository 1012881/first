# add-todo-page — 技术设计

## 概述

采用 Vite + 原生 JavaScript (ES Module) 技术栈构建单页面 Todo 应用。使用函数式编程风格，纯函数管理状态，不可变数据更新。

## 架构决策

| 决策 | 选择 | 理由 |
|------|------|------|
| 构建工具 | Vite | 快速开发服务器，原生 ES Module 支持 |
| UI 框架 | 原生 DOM API | 项目技术栈待定，避免过早引入框架依赖 |
| 状态管理 | 函数式状态容器 | 符合项目函数式编程规范，纯函数管理状态 |
| 数据持久化 | localStorage | 简单可靠，无需后端 |
| 样式方案 | 原生 CSS | 轻量，无需额外依赖 |

## 实现方案

### 文件结构

```
src/
├── index.html          # 入口 HTML
├── js/
│   ├── main.js         # 应用入口，挂载组件
│   ├── store.js        # 函数式状态管理
│   ├── view.js         # DOM 渲染函数
│   └── utils.js        # 工具函数
└── css/
    └── style.css       # 样式

tests/
└── todo.test.js        # 单元测试
```

### 数据流

```
用户操作 → 事件处理 → 状态更新(纯函数) → 重新渲染(纯函数) → DOM 更新
                                    ↕
                              localStorage
```

### 状态模型

```js
// 应用状态 (不可变)
const state = {
  todos: [],           // { id, text, completed, createdAt }
  filter: 'all'        // 'all' | 'active' | 'completed'
}
```

### 核心函数签名

```js
// store.js - 状态管理
createStore(initialState) → { getState, dispatch }
reducer(state, action) → newState

// view.js - 渲染
render(state, container) → void
createTodoElement(todo, dispatch) → HTMLElement

// utils.js - 工具
generateId() → string
saveToStorage(state) → void
loadFromStorage() → state | null
```

## 数据模型

```js
Todo {
  id: string,          // UUID
  text: string,        // 待办内容
  completed: boolean,  // 完成状态
  createdAt: number    // 创建时间戳
}
```

## API / 接口

### Actions (状态变更事件)

```js
{ type: 'ADD_TODO', payload: { text: string } }
{ type: 'TOGGLE_TODO', payload: { id: string } }
{ type: 'DELETE_TODO', payload: { id: string } }
{ type: 'SET_FILTER', payload: { filter: string } }
{ type: 'CLEAR_COMPLETED' }
```

## 依赖

- Vite (devDependency) — 开发服务器和构建

## 风险与缓解

| 风险 | 缓解措施 |
|------|----------|
| localStorage 容量限制 | Todo 数据量小，正常使用不会超出 5MB 限制 |
| 浏览器兼容性 | 使用标准 ES6+ API，Vite 构建时自动处理兼容 |
