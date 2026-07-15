## 1. Backend Project Setup

- [ ] 1.1 Initialize Spring Boot project with pom.xml (spring-boot-starter-web, mybatis-plus, mysql, security, jjwt, lombok)
- [ ] 1.2 Create application.yml with MySQL connection, JWT secret, file upload config
- [ ] 1.3 Create schema.sql with all 5 tables (user, category, article, tag, article_tag)
- [ ] 1.4 Create WikiApplication.java main class and verify startup

## 2. Backend Common Infrastructure

- [ ] 2.1 Create Result.java unified response wrapper (code, message, data)
- [ ] 2.2 Create GlobalExceptionHandler.java with @RestControllerAdvice
- [ ] 2.3 Create CorsConfig.java allowing frontend origin

## 3. User Auth Backend

- [ ] 3.1 Create User entity with @TableName mapping
- [ ] 3.2 Create UserMapper extends BaseMapper<User>
- [ ] 3.3 Create JwtUtils with token generation and validation methods
- [ ] 3.4 Create JwtAuthFilter extends OncePerRequestFilter
- [ ] 3.5 Create SecurityConfig with BCrypt PasswordEncoder and filter chain
- [ ] 3.6 Create AuthController with /api/auth/register and /api/auth/login endpoints
- [ ] 3.7 Create AuthService with register (BCrypt + duplicate check) and login (verify + JWT) logic
- [ ] 3.8 Test: register new user, login with credentials, access protected endpoint

## 4. Category Management Backend

- [ ] 4.1 Create Category entity with @TableName mapping
- [ ] 4.2 Create CategoryMapper extends BaseMapper<Category>
- [ ] 4.3 Create CategoryService with buildTree recursive method
- [ ] 4.4 Create CategoryController with GET /api/categories (tree), POST, PUT /{id}, DELETE /{id} (cascade)
- [ ] 4.5 Test: create root category, create sub-category, rename, delete with cascade

## 5. Tag Management Backend

- [ ] 5.1 Create Tag entity with @TableName mapping
- [ ] 5.2 Create TagMapper extends BaseMapper<Tag>
- [ ] 5.3 Create TagController with GET /api/tags (list by user), POST (create), DELETE /{id}
- [ ] 5.4 Create TagService with duplicate name check and cascade article_tag cleanup on delete
- [ ] 5.5 Test: create tags, list tags, delete tag with associations

## 6. Article Management Backend

- [ ] 6.1 Create Article entity and ArticleTag entity with @TableName mappings
- [ ] 6.2 Create ArticleMapper with custom paginated query method (filter + keyword LIKE + tag JOIN)
- [ ] 6.3 Create ArticleService with create/update/delete logic and tag association management
- [ ] 6.4 Create ArticleController with GET (list with filters), GET /{id} (detail + view count), POST, PUT /{id}, DELETE /{id}
- [ ] 6.5 Test: CRUD articles, filter by category/tag/keyword, verify view count increment

## 7. File Upload Backend

- [ ] 7.1 Create UploadController with POST /api/upload/image
- [ ] 7.2 Create FileService with file type validation, size check (5MB), UUID filename
- [ ] 7.3 Configure static resource mapping for /uploads/** paths
- [ ] 7.4 Test: upload image, verify accessible URL

## 8. Frontend Project Setup

- [ ] 8.1 Create Vite + Vue3 project with Element Plus, Pinia, Vue Router, Axios, TipTap
- [ ] 8.2 Configure vite.config.ts with proxy to localhost:8080
- [ ] 8.3 Create src/api/request.ts with axios instance and JWT interceptor
- [ ] 8.4 Create router/index.ts with all routes and navigation guard (redirect to /login if no token)
- [ ] 8.5 Create App.vue with <router-view> and global SCSS

## 9. Auth Pages Frontend

- [ ] 9.1 Create useAuthStore with login/register/logout actions and token persistence in localStorage
- [ ] 9.2 Create LoginView.vue with Element Plus form (username + password)
- [ ] 9.3 Create RegisterView.vue with Element Plus form (username + password + nickname)
- [ ] 9.4 Test: register, login, verify redirect to /articles, logout

## 10. Main Layout Frontend

- [ ] 10.1 Create MainLayout.vue with left sidebar + top header + <router-view> container
- [ ] 10.2 Create HeaderBar.vue with SearchInput (el-input with @keyup.enter navigation) and UserDropdown (el-dropdown with logout)
- [ ] 10.3 Create SideBar.vue container integrating CategoryTree and user info

## 11. Category Tree Component

- [ ] 11.1 Create useCategoryStore with loadTree action (GET /api/categories)
- [ ] 11.2 Create CategoryTree.vue using el-tree with lazy=false, node-click navigates to /articles?categoryId=X
- [ ] 11.3 Add right-click context menu (el-popover) for create sub-category, rename, delete
- [ ] 11.4 Test: load tree, click to filter articles, create/rename/delete categories

## 12. Article List Page

- [ ] 12.1 Create useArticleStore with fetchList action and useTagStore with fetchTags action
- [ ] 12.2 Create ArticleList.vue with el-table (title, tags, category, updatedAt) and pagination
- [ ] 12.3 Create TagFilter.vue with el-tag selectable list, sync to route query
- [ ] 12.4 Create ArticleCard.vue as clickable row linking to /article/:id
- [ ] 12.5 Wire categoryId/tagId/keyword route query params to API filters
- [ ] 12.6 Add "New Article" button linking to /article/create

## 13. Article Editor Page (TipTap)

- [ ] 13.1 Create TipTapEditor.vue wrapping @tiptap/vue-3 with StarterKit, Image extension
- [ ] 13.2 Configure image upload: on image drop/paste, call POST /api/upload/image and insert returned URL
- [ ] 13.3 Create CategorySelector.vue with el-select loading categories
- [ ] 13.4 Create ArticleEditor.vue with el-form (title input + CategorySelector + TipTapEditor + el-tag-select for tags + status radio)
- [ ] 13.5 Handle create mode (/article/create): POST /api/articles on save
- [ ] 13.6 Handle edit mode (/article/:id/edit): GET article detail, populate form, PUT on save
- [ ] 13.7 Test: create article with rich text + image + tags, edit and update

## 14. Article Detail Page

- [ ] 14.1 Create ArticleDetail.vue with title, category breadcrumb, tag list, publish time, view count, HTML content (v-html)
- [ ] 14.2 Add "Edit" button linking to /article/:id/edit
- [ ] 14.3 Add "Delete" button with confirmation dialog and redirect to /articles
- [ ] 14.4 Test: view article, verify view count increment, edit/delete

## 15. Integration & Polish

- [ ] 15.1 Wire HeaderBar search to navigate to /articles?keyword=xxx
- [ ] 15.2 Add loading states (el-skeleton) to ArticleList and ArticleDetail
- [ ] 15.3 Add empty states (el-empty) to ArticleList when no results
- [ ] 15.4 Style TipTap editor content rendering in ArticleDetail
- [ ] 15.5 End-to-end test: register → login → create category → create article with tags → search → edit → delete
