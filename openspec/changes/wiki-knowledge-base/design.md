## Context

当前项目为空脚手架（仅有 SDD Harness 基础结构：OpenSpec + Superpowers + Qoder 集成）。需要在其中构建一个完整的 Wiki 知识库系统，采用前后端分离架构。目标用户为个人，对并发和分布式无特殊要求。

## Goals / Non-Goals

**Goals:**
- 提供用户注册/登录，JWT 鉴权
- 支持无限级树形分类目录管理
- 提供所见即所得富文本文章编辑
- 支持文章多标签关联和交叉检索
- 全文搜索 + 分类/标签筛选
- 所有数据按用户隔离

**Non-Goals:**
- 不实现多人协作、评论、版本历史
- 不实现 Markdown 编辑器（仅富文本）
- 不实现文件附件上传（仅图片）
- 不实现 OAuth/第三方登录
- 不实现国际化（仅中文）

## Decisions

### 后端: Spring Boot 3 + MyBatis-Plus

**选择 MyBatis-Plus 而非 JPA 的原因**：分类树需要递归查询构建嵌套结构，标签需要动态多对多关联查询。MyBatis-Plus 的自定义 SQL 更灵活直观。

### 前端: Vue3 + Element Plus + TipTap

**选择 TipTap 而非 Quill**：TipTap 基于 ProseMirror，扩展机制更强（自定义节点/插件），对图片上传的支持更完善，Vue3 生态更好。

### 分类树: parent_id 邻接表模型

**选择邻接表而非嵌套集/闭包表**：个人 Wiki 分类层级不深（通常 2-3 层），数据量小。邻接表最简单，MyBatis-Plus 递归查询即可构建树，无需额外维护左右值。

### 富文本存储: LONGTEXT 存 HTML

直接存储 HTML 而非 Markdown 或 JSON。读取时无需转换即可渲染，创建时 TipTap 直接输出 HTML。MySQL LONGTEXT 最大 4GB 足够。

### 图片上传: 本地磁盘存储

个人项目无需 OSS。图片存后端 `uploads/` 目录，通过 Spring Boot 静态资源映射访问。

## Risks / Trade-offs

- [分类删除级联] → 删除父分类时级联删除子分类和所有文章，需前端二次确认弹窗
- [图片清理] → 文章删除后关联图片不会自动清理，首次迭代可接受，后期可加定时清理
- [全文搜索性能] → MySQL LIKE 在数据量 < 10 万条时性能足够，后期可迁移 Elasticsearch
- [富文本 XSS] → HTML 直接存储存在 XSS 风险，前端用 v-html 渲染时注意：TipTap 自带内容过滤，后端不做清洗
