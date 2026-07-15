## Why

个人需要一个结构化的知识管理系统来组织和检索学习笔记、技术文档和项目经验。现有的笔记工具缺乏树形分类与标签交叉检索的结合能力，且数据不自主可控。自建 Wiki 系统可完全掌握数据，按需定制。

## What Changes

- 新增用户注册与登录功能，基于 JWT 令牌认证
- 新增无限级树形分类目录，支持拖拽排序和右键操作
- 新增富文本文章编辑器（TipTap），支持图片上传
- 新增标签系统，支持文章多标签关联和按标签筛选
- 新增全文搜索和多维筛选（分类 + 标签 + 关键字）
- 所有数据按用户隔离，单用户数据完全独立

## Capabilities

### New Capabilities

- `user-auth`: 用户注册、登录、JWT 令牌认证与鉴权
- `category-management`: 无限级树形分类目录的 CRUD，递归嵌套结构
- `article-management`: 文章的创建、编辑、删除、发布，含富文本内容存储和分类归属
- `tag-management`: 标签的创建、删除，文章与标签的多对多关联
- `content-search`: 文章全文搜索，按分类/标签/关键字多维筛选与分页
- `file-upload`: 富文本编辑器内图片上传，返回可访问 URL

### Modified Capabilities

<!-- 新项目，无已有规范需要修改 -->

## Impact

- 新建项目 `backend/` (Spring Boot 3 + MyBatis-Plus + MySQL)
- 新建项目 `frontend/` (Vue3 + Vite + Element Plus + TipTap)
- 新增 MySQL 数据库 `wiki_db`，5 张表
- 新增 15 个 REST API 端点
- 前端新增 6 个页面、12 个组件
- 无外部依赖系统影响
