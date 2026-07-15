# Wiki 知识库系统设计文档

## 概述

Spring Boot + Vue3 前后端分离的个人知识管理 Wiki 系统。

## 技术选型

| 层 | 技术 |
|----|------|
| 后端框架 | Spring Boot 3 |
| 安全 | Spring Security + JWT |
| ORM | MyBatis-Plus |
| 数据库 | MySQL |
| 前端框架 | Vue3 + Vite |
| UI 组件库 | Element Plus |
| 富文本编辑器 | TipTap (ProseMirror) |
| 状态管理 | Pinia |
| HTTP 客户端 | Axios |

## 数据库设计

### user 用户表
| 字段 | 类型 | 说明 |
|------|------|------|
| id | BIGINT | 主键 |
| username | VARCHAR(50) | 用户名，唯一 |
| password | VARCHAR(255) | BCrypt 加密 |
| nickname | VARCHAR(50) | 昵称 |
| avatar | VARCHAR(255) | 头像 URL |
| created_at/updated_at | DATETIME | 时间戳 |

### category 分类表（树形结构）
| 字段 | 类型 | 说明 |
|------|------|------|
| id | BIGINT | 主键 |
| name | VARCHAR(50) | 分类名 |
| parent_id | BIGINT | 父级 ID，0 为根节点 |
| sort_order | INT | 排序 |
| user_id | BIGINT | 所属用户 |

### article 文章表
| 字段 | 类型 | 说明 |
|------|------|------|
| id | BIGINT | 主键 |
| title | VARCHAR(200) | 标题 |
| content | LONGTEXT | 富文本 HTML |
| category_id | BIGINT | 所属分类 |
| user_id | BIGINT | 作者 |
| status | TINYINT | 0=草稿, 1=已发布 |
| view_count | INT | 阅读数 |
| created_at/updated_at | DATETIME | 时间戳 |

### tag 标签表
| 字段 | 类型 | 说明 |
|------|------|------|
| id | BIGINT | 主键 |
| name | VARCHAR(30) | 标签名，唯一 |
| user_id | BIGINT | 所属用户 |

### article_tag 文章标签关联表
| 字段 | 类型 | 说明 |
|------|------|------|
| article_id | BIGINT | 文章 ID |
| tag_id | BIGINT | 标签 ID |
| 联合主键 | | (article_id, tag_id) |

## API 设计

### 认证 `/api/auth`
- `POST /api/auth/register` — 注册
- `POST /api/auth/login` — 登录，返回 JWT

### 分类 `/api/categories`
- `GET /api/categories` — 用户分类树（递归嵌套）
- `POST /api/categories` — 新建
- `PUT /api/categories/{id}` — 重命名
- `DELETE /api/categories/{id}` — 删除（级联）

### 文章 `/api/articles`
- `GET /api/articles?categoryId=&keyword=&tagId=&page=&size=` — 分页列表+筛选
- `GET /api/articles/{id}` — 详情（含标签）
- `POST /api/articles` — 创建
- `PUT /api/articles/{id}` — 更新（含标签变更）
- `DELETE /api/articles/{id}` — 删除

### 标签 `/api/tags`
- `GET /api/tags` — 用户标签列表
- `POST /api/tags` — 创建
- `DELETE /api/tags/{id}` — 删除（级联清理）

### 上传 `/api/upload`
- `POST /api/upload/image` — 图片上传，返回 URL

### 全局规范
- 统一响应：`{ code, message, data }`
- 鉴权：Header `Authorization: Bearer <token>`
- 数据隔离：按 user_id 自动过滤

## 前端设计

### 路由
```
/login              → 登录
/register           → 注册
/                   → 主布局（侧边栏 + 内容）
  /articles         → 文章列表（分类/标签/搜索筛选）
  /article/:id      → 阅读
  /article/create   → 新建
  /article/:id/edit → 编辑
```

### 核心组件
- SideBar.vue → CategoryTree.vue（el-tree 右键操作）
- HeaderBar.vue → SearchInput + UserDropdown
- ArticleList.vue → ArticleCard + TagFilter
- ArticleDetail.vue → TagList
- ArticleEditor.vue → TipTapEditor + CategorySelector

### 状态管理
- useAuthStore — 登录态
- useCategoryStore — 分类树
- useArticleStore — 文章 CRUD
- useTagStore — 标签列表

## 项目结构

```
backend/   → Spring Boot 后端（com.wiki.*）
frontend/  → Vue3 前端（Vite + Element Plus + TipTap）
```

详见 controller/service/mapper/entity 分层和前端 api/stores/views/components 分层。
