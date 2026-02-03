---
layout: post
title: "使用 Claude Code 提升编码能力完全指南"
subtitle: "面向有经验开发者的 Claude Code 实战教程"
date: 2026-01-30
author: "toboto"
tags:
    - Claude Code
    - AI编程
    - 开发工具
    - 效率提升
---

# 使用 Claude Code 提升编码能力完全指南

## 目录

1. [Claude Code 简介](#1-claude-code-简介)
2. [安装与配置](#2-安装与配置)
3. [在不同环境中使用 Claude Code](#3-在不同环境中使用-claude-code)
4. [Claude Code 的工作模式](#4-claude-code-的工作模式)
5. [初始化新项目](#5-初始化新项目)
6. [接手既有项目](#6-接手既有项目)
7. [MCP (Model Context Protocol) 深度应用](#7-mcp-model-context-protocol-深度应用)
8. [Skills 技能系统](#8-skills-技能系统)
9. [全自动化开发流程](#9-全自动化开发流程)
10. [权限管理与安全](#10-权限管理与安全)
11. [最佳实践与进阶技巧](#11-最佳实践与进阶技巧)

---

## 1. Claude Code 简介

### 1.1 什么是 Claude Code

Claude Code 是 Anthropic 推出的官方命令行工具，专为软件开发场景设计。它不同于通用的 Claude 聊天界面，而是深度集成了开发工作流，能够：

- 直接读取和修改代码文件
- 执行终端命令
- 理解项目结构和上下文
- 自动化开发流程
- 集成开发工具链

### 1.2 为什么选择 Claude Code

对于有 5 年以上开发经验的工程师，Claude Code 的价值在于：

- **减少重复劳动**：自动生成样板代码、测试用例、文档
- **快速学习新技术栈**：理解陌生代码库，快速上手新项目
- **提升代码质量**：自动化测试、代码审查、重构建议
- **加速开发流程**：从需求到部署的全流程自动化
- **知识传承**：通过 Skills 和 MCP 构建团队知识库

### 1.3 适用场景

- Java/PHP/TypeScript/JavaScript/Python/Golang 项目开发
- Vue + Ant Design 前端应用
- Spring Boot 后端服务
- 微服务架构
- CI/CD 流程优化
- 代码审查和重构

---

## 2. 安装与配置

### 2.1 系统要求

- macOS, Linux, or Windows (WSL)
- Node.js 18+ (推荐使用 nvm 管理)
- Git 2.0+
- 有效的 Anthropic API 密钥

### 2.2 安装步骤

```bash
# 使用 npm 安装
npm install -g @anthropic-ai/claude-code

# 或使用 yarn
yarn global add @anthropic-ai/claude-code

# 验证安装
claude --version
```

### 2.3 初始化配置

```bash
# 第一次运行，配置 API 密钥
claude config set apiKey YOUR_API_KEY

# 配置默认模型（推荐 sonnet 平衡性能和成本）
claude config set model sonnet

# 查看所有配置
claude config list
```

### 2.4 配置文件说明

Claude Code 的配置文件位于 `~/.claude/`：

- `config.json` - 全局配置
- `keybindings.json` - 键盘快捷键
- `skills/` - 自定义 Skills
- `mcp-config.json` - MCP 服务器配置

---

## 3. 在不同环境中使用 Claude Code

### 3.1 命令行模式

#### 3.1.1 基础使用

```bash
# 启动交互式会话
claude

# 在特定项目目录中启动
cd /path/to/project
claude

# 直接执行任务
claude "帮我分析这个项目的依赖关系"
```

#### 3.1.2 常用命令

```bash
# 查看帮助
/help

# 清空对话历史
/clear

# 切换模型
/model opus  # 使用更强大的模型
/model haiku # 使用更快速的模型

# 查看可用的 Skills
/skills

# 查看 MCP 服务器状态
/mcp
```

#### 3.1.3 实用命令详解

**1. /resume - 恢复之前的会话**

```bash
# 场景：你关闭了 Claude Code，想继续之前未完成的工作
/resume

# Claude 会列出最近的会话，选择一个继续
# 这样可以保持上下文连续性，非常适合长期项目开发
```

**用途：**
- 继续未完成的重构任务
- 恢复中断的调试会话
- 查看之前的对话记录

**2. /init - 初始化新项目**

```bash
# 快速初始化一个新项目
/init

# Claude 会引导你：
# - 选择项目类型（Web应用、CLI工具、库等）
# - 选择技术栈（React/Vue, Node/Python等）
# - 设置项目结构
# - 生成基础配置文件
```

**示例对话：**
```
用户: /init
Claude: 我来帮你初始化一个新项目。请选择项目类型：
  1. Web 应用
  2. CLI 工具
  3. 库/包
  4. 微服务

用户: 1
Claude: 选择前端框架：
  1. React + TypeScript
  2. Vue 3 + TypeScript
  3. Next.js
  4. 原生 HTML/JS

用户: 2
Claude: 选择后端（可选）：
  1. Node.js (Express)
  2. Python (FastAPI)
  3. Java (Spring Boot)
  4. 无后端（纯前端）

[继续配置并生成项目结构...]
```

**3. /task - 任务管理**

```bash
# 查看当前任务列表
/task

# 创建新任务
/task add "实现用户认证功能"

# 标记任务完成
/task done 1

# 查看任务详情
/task show 1
```

**用途：**
- 将大型功能分解为小任务
- 跟踪开发进度
- 多人协作时明确分工

**4. /commit - 智能提交（Skill）**

```bash
# 自动分析变更并生成提交信息
/commit

# Claude 会：
# 1. 检查 git status
# 2. 分析变更内容
# 3. 生成符合规范的提交信息
# 4. 征求确认后提交
```

**5. /search - 代码搜索**

```bash
# 在代码库中搜索
/search "用户认证"

# 支持正则表达式
/search "function.*Auth"

# 限定文件类型
/search "API" --type=ts
```

**6. /explain - 代码解释**

```bash
# 解释选中的代码或文件
/explain src/auth/login.ts

# 生成详细的代码文档
/explain --detailed src/core/engine.ts
```

**7. /test - 生成测试**

```bash
# 为指定文件生成测试
/test src/utils/validator.ts

# 指定测试框架
/test --framework=jest src/api/user.ts
```

**8. /review - 代码审查**

```bash
# 审查当前变更
/review

# 审查指定文件
/review src/components/UserForm.tsx

# 审查 Pull Request
/review-pr 123
```

### 3.2 VS Code 集成

#### 3.2.1 安装 VS Code 扩展

1. 在 VS Code 扩展市场搜索 "Claude Code"
2. 安装官方扩展
3. 重启 VS Code

#### 3.2.2 配置 VS Code

在 VS Code 设置中配置：

```json
{
  "claude.apiKey": "YOUR_API_KEY",
  "claude.model": "sonnet",
  "claude.autoSuggest": true,
  "claude.inlineCompletion": true
}
```

#### 3.2.3 VS Code 中的使用方式

- **侧边栏聊天**：点击 Claude 图标打开聊天面板
- **内联建议**：编辑时自动提供代码建议
- **快捷键**：
  - `Cmd+Shift+C` (Mac) / `Ctrl+Shift+C` (Win) - 打开 Claude
  - `Cmd+K` - 对选中代码提问
  - `Cmd+I` - 内联编辑

#### 3.2.4 VS Code 优势

- 可视化文件浏览
- 代码高亮和自动补全
- 集成调试器
- Git 可视化界面
- 多文件同时编辑

### 3.3 命令行 vs VS Code 选择建议

| 场景 | 推荐方式 | 理由 |
|------|---------|------|
| 快速脚本任务 | 命令行 | 启动快速，专注任务 |
| 大型项目开发 | VS Code | 可视化更好，易于导航 |
| 服务器环境 | 命令行 | 通常没有 GUI |
| 代码审查 | VS Code | 并排对比更直观 |
| CI/CD 集成 | 命令行 | 易于脚本化 |
| 学习新项目 | VS Code | 文件树帮助理解结构 |

---

## 4. Claude Code 的工作模式

Claude Code 支持三种工作模式，每种模式都有其特定的应用场景和特点。理解这些模式的差异以及如何在它们之间切换，是高效使用 Claude Code 的关键。

### 4.1 对话模式 (Conversation Mode)

#### 4.1.1 模式特点

对话模式是 Claude Code 的默认模式，适合探索性、交互式的开发任务。在这个模式下，Claude 会：

- 逐步响应你的问题
- 根据你的反馈调整方向
- 提供建议供你选择
- 在不确定时向你询问

**适用场景：**
- 探索性问题（"这个框架是如何工作的？"）
- 代码讲解（"解释这段代码的逻辑"）
- 架构讨论（"我应该使用微服务还是单体架构？"）
- 需求澄清（"这个功能应该怎样实现？"）
- 快速代码修改（"修复这个语法错误"）
- 学习新概念（"什么是依赖注入？"）

#### 4.1.2 使用示例

```bash
用户: 这个函数的时间复杂度是多少？

Claude: 让我分析一下这个函数...

时间复杂度分析：
- 外层循环：O(n)
- 内层循环：最坏情况 O(n)
- 总体：O(n²)

这是一个嵌套循环，时间复杂度为 **O(n²)**

优化建议：
可以使用 HashSet 将时间复杂度降至 O(n)，需要我展示优化后的代码吗？
```

#### 4.1.3 多模态上下文素材

在对话模式下，你可以通过多种方式为 Claude 提供上下文信息：

**1. 引用文件**

```bash
# 方式一：直接在对话中提及文件路径
用户: 分析 src/services/UserService.java 的性能问题

# 方式二：使用 @ 符号引用
用户: @src/services/UserService.java 这个文件有哪些可以优化的地方？

# 方式三：引用多个文件
用户: 比较 @UserService.java 和 @OrderService.java 的实现差异
```

**2. 复制剪贴板图片**

```bash
# 在 VS Code 中
1. 截图或复制图片到剪贴板
2. 在 Claude Code 对话中粘贴（Cmd+V / Ctrl+V）
3. Claude 会自动分析图片内容

示例场景：
- 粘贴 UI 设计稿，让 Claude 生成对应的前端代码
- 粘贴错误截图，让 Claude 诊断问题
- 粘贴架构图，让 Claude 理解系统设计
- 粘贴数据表设计图，让 Claude 生成实体类

用户: [粘贴 UI 设计图]
用户: 根据这个设计图实现用户列表页面

Claude: 我看到了一个用户列表页面的设计：
- 顶部有搜索框和筛选器
- 表格包含：头像、姓名、邮箱、角色、状态、操作列
- 底部有分页控件

我将使用 Vue 3 + Ant Design Vue 实现这个页面...
[生成代码]
```

**3. 复制剪贴板文字**

```bash
# 场景一：复制错误日志
用户: [粘贴错误日志]
NullPointerException at line 156
    at com.example.OrderService.calculatePrice(OrderService.java:156)
    at com.example.OrderController.createOrder(OrderController.java:89)

用户: 这个错误是什么原因？

# 场景二：复制代码片段
用户: [从 Stack Overflow 复制代码]
用户: 这段代码能用在我们的项目中吗？需要什么调整？

# 场景三：复制配置文件内容
用户: [粘贴 application.yml]
用户: 检查这个配置是否有问题
```

**4. 使用外部链接**

```bash
# 引用 GitHub Issues/PRs
用户: 查看 https://github.com/username/project/issues/123
用户: 这个 issue 提到的问题应该如何解决？

# 引用文档
用户: 参考 https://spring.io/guides/gs/rest-service/
用户: 按照这个教程的方式实现我们的 REST API

# 引用技术博客
用户: 根据 https://medium.com/article-url 这篇文章的方法优化我们的数据库查询
```

**5. 组合使用多种上下文**

```bash
用户: 我要实现一个新功能
[粘贴需求文档图片]
参考这个开源项目的实现: https://github.com/example/similar-project
需要修改的文件: @src/services/OrderService.java
[粘贴现有代码片段]
```

### 4.2 计划模式 (Plan Mode)

#### 4.2.1 模式特点

计划模式是 Claude Code 的智能规划模式，适合复杂的、多步骤的开发任务。在这个模式下，Claude 会：

- 全面分析任务需求
- 探索代码库结构
- 制定详细的执行计划
- 向你展示计划并征求确认
- 按计划执行并报告进度
- 遇到问题时调整计划

**自动进入计划模式的场景：**
- 多文件修改任务（"添加用户认证模块"）
- 架构变更（"将单体应用拆分为微服务"）
- 新功能开发（"实现支付功能"）
- 大规模重构（"优化整个服务层"）
- 数据库迁移（"迁移到新的数据库架构"）

#### 4.2.2 工作流程详解

```bash
用户: 帮我添加用户认证功能

Claude: 这是一个复杂任务，我将进入计划模式。

[Phase 1: 探索阶段]
正在探索代码库...
✓ 发现现有项目结构
✓ 识别技术栈：Spring Boot + Vue 3
✓ 分析现有的用户模块

[Phase 2: 规划阶段]
【计划概述】
实现基于 JWT 的用户认证系统

【详细步骤】
1. 后端部分 (预计 6 个文件)
   ├─ SecurityConfig.java: 配置 Spring Security
   ├─ JwtTokenProvider.java: JWT 工具类
   └─ AuthController.java: 登录/注册接口

2. 前端部分 (预计 5 个文件)
   ├─ api/auth.ts: 认证 API 调用
   ├─ views/Login.vue: 登录页面
   └─ store/auth.ts: 用户状态

是否执行此计划？(yes/no/modify)

用户: yes

[Phase 3: 执行阶段]
[1/11] 添加 Maven 依赖...
✓ pom.xml 已更新

[2/11] 创建 SecurityConfig.java...
✓ 文件已创建

...

执行完成！
```

#### 4.2.3 手动进入计划模式

```bash
# 使用 --plan 标志
claude --plan "重构订单服务"

# 在对话中明确要求
用户: 请使用计划模式来实现这个功能...
```

#### 4.2.4 计划模式的优势

1. **全局视角**：Claude 会先理解整个项目再动手
2. **风险识别**：提前发现潜在问题
3. **可控性**：计划经过你确认才执行
4. **可追踪**：清晰的进度报告
5. **可调整**：执行过程中可以修改计划

### 4.3 自主模式 (Autonomous Mode)

#### 4.3.1 模式特点

自主模式是 Claude Code 的全自动模式，适合明确定义、不需要人工干预的任务。在这个模式下，Claude 会：

- 自主做出所有技术决策
- 最小化用户交互
- 持续执行直到任务完成
- 自动处理遇到的问题

**适用场景：**
- 批量任务（"为所有 API 添加 OpenAPI 文档"）
- 标准化操作（"统一所有文件的代码风格"）
- 自动化测试（"生成缺失的单元测试"）
- 文档生成（"为所有公共方法添加 JavaDoc"）

#### 4.3.2 启用自主模式

```bash
# 基本语法
claude --autonomous "任务描述"

# 示例：批量添加测试
claude --autonomous "为 services 目录下所有类生成单元测试，覆盖率达到 80%"

Claude: [自主模式启动]
扫描 services 目录...
找到 23 个 Service 类

[1/23] UserService
  ✓ 生成 UserServiceTest.java (12 个测试用例)
  ✓ 覆盖率: 87%

...

[23/23] 完成
总计: 23 个测试文件，347 个测试用例
平均覆盖率: 86%
```

#### 4.3.3 注意事项

**使用自主模式前的检查：**

- [ ] 任务目标明确，无歧义
- [ ] 项目已提交到 Git（可随时回滚）
- [ ] 不涉及生产环境操作
- [ ] 已配置合理的权限限制

**不适合自主模式的场景：**
- ❌ 生产环境部署
- ❌ 数据库删除操作
- ❌ 需要业务判断的任务
- ❌ 不可逆的破坏性操作

### 4.4 模式切换

#### 4.4.1 自动切换

Claude Code 会根据任务复杂度自动切换模式：

```bash
# 简单问题 → 对话模式
用户: 这个变量的类型是什么？
[保持对话模式]

# 复杂任务 → 自动切换到计划模式
用户: 添加完整的用户权限管理系统
Claude: 这是一个复杂任务，我将切换到计划模式...
```

#### 4.4.2 手动切换

```bash
# 切换到计划模式
用户: /plan 实现这个功能

# 退出计划模式
用户: /exit-plan

# 切换到自主模式（需要重启）
claude --autonomous "任务描述"
```

### 4.5 工作模式选择策略

| 任务类型 | 推荐模式 | 示例 | 选择理由 |
|---------|---------|------|---------|
| 询问理解 | 对话模式 | "这段代码做什么？" | 简单交互即可 |
| 单文件修改 | 对话模式 | "修复这个 bug" | 影响范围小 |
| 代码解释 | 对话模式 | "解释这个算法" | 需要互动讨论 |
| 多文件功能 | 计划模式 | "添加支付模块" | 需要整体规划 |
| 架构变更 | 计划模式 | "重构服务层" | 影响范围大 |
| 批量任务 | 自主模式 | "为所有 API 添加文档" | 明确且重复 |
| 代码风格统一 | 自主模式 | "格式化所有代码" | 标准化操作 |
| 探索学习 | 对话模式 | "项目架构是怎样的？" | 需要逐步深入 |

---

## 5. 初始化新项目

### 5.1 从零开始创建项目

#### 5.1.1 明确技术栈

```bash
claude

用户: 我要创建一个电商系统，帮我确定技术栈。要求：
- 前端用 Vue 3 + Ant Design Vue
- 后端用 Spring Boot
- 支持微服务架构
- 需要 Redis 缓存
- 使用 MySQL 数据库

Claude: 我建议以下技术栈：

前端：
- Vue 3.4+ (Composition API)
- Ant Design Vue 4.x
- Vite 5.x (构建工具)
- Pinia (状态管理)
- Vue Router 4.x
- Axios (HTTP 客户端)
- TypeScript 5.x

后端：
- Spring Boot 3.2
- Spring Cloud 2023.0.x (微服务组件)
- Spring Cloud Gateway (API 网关)
- Spring Cloud Alibaba Nacos (服务注册发现)
- MyBatis Plus 3.5 (ORM)
- MySQL 8.0
- Redis 7.x
- RabbitMQ (消息队列)
- JWT (认证)

开发工具：
- Maven 3.9
- Docker & Docker Compose
- Git

是否确认这个技术栈？需要调整吗？
```

#### 5.1.2 自动生成项目结构

```bash
用户: 确认。请帮我初始化整个项目结构。

Claude: 我将创建以下结构：

ecommerce-system/
├── frontend/              # Vue 前端
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── vite.config.ts
├── services/              # 微服务
│   ├── user-service/      # 用户服务
│   ├── product-service/   # 商品服务
│   ├── order-service/     # 订单服务
│   └── gateway/           # API 网关
├── common/                # 公共模块
│   ├── common-core/
│   └── common-security/
├── docker/                # Docker 配置
│   └── docker-compose.yml
└── README.md

[Claude 自动创建所有文件和配置]
```

### 5.2 配置项目规范

#### 5.2.1 代码风格配置

```bash
用户: 配置代码规范和 lint 工具

Claude: [创建以下配置]
- .editorconfig
- .eslintrc.js (前端)
- .prettierrc
- checkstyle.xml (后端 Java)
- .gitignore
```

#### 5.2.2 Git Hooks 配置

```bash
Claude: 我已配置 Git Hooks：
- pre-commit: 运行 lint 检查
- commit-msg: 验证提交信息格式
- pre-push: 运行单元测试
```

### 5.3 生成基础代码

#### 5.3.1 后端基础结构

```bash
用户: 生成用户服务的基础代码

Claude: [生成以下代码]
user-service/
├── src/main/java/com/example/user/
│   ├── UserServiceApplication.java
│   ├── controller/
│   │   └── UserController.java
│   ├── service/
│   │   ├── UserService.java
│   │   └── impl/UserServiceImpl.java
│   ├── mapper/
│   │   └── UserMapper.java
│   ├── entity/
│   │   └── User.java
│   ├── dto/
│   │   ├── UserDTO.java
│   │   └── UserQueryDTO.java
│   └── config/
│       ├── RedisConfig.java
│       └── SecurityConfig.java
└── src/main/resources/
    ├── application.yml
    └── mapper/
        └── UserMapper.xml
```

#### 5.3.2 前端基础结构

```bash
用户: 生成前端用户管理模块

Claude: [生成以下代码]
frontend/src/
├── views/
│   └── user/
│       ├── UserList.vue
│       ├── UserForm.vue
│       └── UserDetail.vue
├── api/
│   └── user.ts
├── store/
│   └── user.ts
└── router/
    └── user.ts
```

### 5.4 验证项目可运行

```bash
用户: 验证项目能否正常运行

Claude:
[执行以下验证]
1. 检查依赖安装
2. 编译项目
3. 运行测试
4. 启动开发服务器

✓ 用户服务启动成功 (端口 8001)
✓ 前端开发服务器运行 (端口 5173)
✓ 所有测试通过

项目已就绪，可以开始开发！
```

---

## 6. 接手既有项目

### 6.1 理解项目结构

#### 6.1.1 快速概览

```bash
cd existing-project
claude

用户: 帮我理解这个项目的结构

Claude: [使用 Explore agent 分析]
这是一个基于 Spring Boot 的微服务项目：

项目结构：
- 5 个微服务模块
- 使用 Spring Cloud Netflix 技术栈
- MySQL + Redis 存储方案
- 前端使用 Vue 2.x + Element UI

关键模块：
1. gateway-service (端口 8080) - API 网关
2. auth-service (端口 8001) - 认证服务
3. user-service (端口 8002) - 用户管理
4. order-service (端口 8003) - 订单处理
5. product-service (端口 8004) - 商品管理

技术特点：
- 使用 MyBatis 作为 ORM
- Redis 用于缓存和分布式锁
- RabbitMQ 处理异步消息
- JWT 实现认证鉴权
```

#### 6.1.2 深入分析核心模块

```bash
用户: 详细分析订单服务的实现

Claude:
订单服务分析 (order-service):

【数据模型】
- Order (订单主表)
- OrderItem (订单明细)
- OrderStatus (订单状态枚举)

【核心流程】
1. 创建订单
   - 库存检查 (调用 product-service)
   - 价格计算
   - 订单持久化
   - 发送 MQ 消息通知

2. 支付流程
   - 接收支付回调
   - 更新订单状态
   - 触发发货流程

3. 订单查询
   - 多维度查询 (用户ID、订单号、状态等)
   - 分页支持
   - Redis 缓存热点订单

【依赖关系】
- 依赖 product-service 查询商品信息
- 依赖 user-service 验证用户
- 被 gateway 路由

【潜在问题】
⚠ 缺少分布式事务处理
⚠ 订单创建接口没有幂等性保证
⚠ 缺少单元测试覆盖
```

### 6.2 掌握开发规范

#### 6.2.1 识别编码风格

```bash
用户: 这个项目的编码规范是什么？

Claude:
项目编码规范：

【Java 后端】
- 使用驼峰命名
- Controller 方法返回统一包装类 Result<T>
- 异常使用自定义 BusinessException
- 日志使用 SLF4J + Logback
- 注释使用 JavaDoc 格式

【前端】
- Vue 组件使用 PascalCase
- API 调用封装在 /api 目录
- 使用 Vuex 管理全局状态
- 路由懒加载
- 使用 ESLint Standard 规范

【数据库】
- 表名小写 + 下划线
- 主键统一命名 id
- 时间字段: created_at, updated_at
- 逻辑删除字段: deleted (0-未删除, 1-已删除)
```

#### 6.2.2 学习 API 设计模式

```bash
用户: API 接口是如何设计的？

Claude:
API 设计规范：

【RESTful 风格】
GET    /api/orders          # 查询订单列表
GET    /api/orders/{id}     # 查询单个订单
POST   /api/orders          # 创建订单
PUT    /api/orders/{id}     # 更新订单
DELETE /api/orders/{id}     # 删除订单

【统一响应格式】
{
  "code": 200,
  "message": "success",
  "data": {...},
  "timestamp": 1706601234567
}

【分页格式】
{
  "code": 200,
  "data": {
    "records": [...],
    "total": 100,
    "pageNum": 1,
    "pageSize": 10
  }
}
```

### 6.3 在既有项目中开发

#### 6.3.1 添加新功能

```bash
用户: 在订单服务中添加订单导出功能

Claude: [进入计划模式]

我的计划：
1. 分析现有订单查询逻辑
2. 添加导出接口
   - Controller: OrderController.exportOrders()
   - Service: OrderService.exportToExcel()
3. 使用 Apache POI 生成 Excel
4. 添加异步导出支持（大数据量场景）
5. 编写单元测试
6. 更新 API 文档

是否执行？

用户: 确认

Claude: [自动实现所有代码]
✓ 已添加 OrderController.exportOrders()
✓ 已实现 ExcelExportService
✓ 已添加单元测试 (覆盖率 85%)
✓ 已更新 Swagger 文档

新接口：POST /api/orders/export
```

#### 6.3.2 修复 Bug

```bash
用户: 订单创建时库存扣减有并发问题，帮我修复

Claude:
问题分析：
当前实现使用了数据库查询 + 更新的方式，存在竞态条件。

解决方案：
1. 使用 Redis 分布式锁保证原子性
2. 使用数据库乐观锁 (version 字段)
3. 使用 LUA 脚本保证 Redis 操作原子性

推荐方案 2 (数据库乐观锁)：
- 对现有代码改动最小
- 性能可接受
- 无需引入新的中间件

[自动修改代码并添加测试]
```

### 6.4 代码重构

```bash
用户: OrderServiceImpl 太长了（800行），帮我重构

Claude:
重构计划：

【问题识别】
- 单个类承担过多职责
- 订单创建逻辑复杂 (200+ 行)
- 大量重复的数据转换代码

【重构方案】
1. 提取 OrderCreateService 处理订单创建
2. 提取 OrderConverter 处理 DTO 转换
3. 提取 OrderValidator 处理业务校验
4. 使用策略模式处理不同订单类型

[执行重构]
✓ 提取 4 个新服务类
✓ 原 OrderServiceImpl 从 800 行降至 200 行
✓ 单元测试全部通过
✓ 代码可读性提升 60%
```

---

## 7. MCP (Model Context Protocol) 深度应用

### 7.1 什么是 MCP

MCP (Model Context Protocol) 是一个开放协议，允许 Claude Code 连接外部工具和数据源。

**核心概念**：
- **MCP Server**: 提供特定功能的服务（如数据库查询、API 调用）
- **MCP Client**: Claude Code 作为客户端调用 Server
- **Resources**: Server 提供的数据资源
- **Tools**: Server 提供的可执行工具
- **Prompts**: Server 提供的提示模板

### 7.2 配置 MCP

#### 7.2.1 MCP 配置文件

编辑 `~/.claude/mcp-config.json`:

```json
{
  "mcpServers": {
    "mysql": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-mysql",
        "mysql://user:password@localhost:3306/mydb"
      ]
    },
    "gitlab": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-gitlab"
      ],
      "env": {
        "GITLAB_TOKEN": "your-gitlab-token",
        "GITLAB_URL": "https://gitlab.example.com"
      }
    },
    "github": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-github"
      ],
      "env": {
        "GITHUB_TOKEN": "your-github-token"
      }
    }
  }
}
```

### 7.3 实用 MCP Server 示例

#### 7.3.1 MySQL MCP 详细配置和使用

MySQL MCP 是最常用的 MCP Server 之一，允许 Claude Code 直接连接和操作 MySQL 数据库。

**第一步：安装配置**

1. **安装 MySQL MCP Server**

```bash
# 使用 npx 运行（推荐，无需安装）
# 在配置文件中使用 npx 会自动下载和运行

# 或全局安装
npm install -g @modelcontextprotocol/server-mysql
```

2. **配置 MCP 服务器**

编辑 `~/.claude/mcp-config.json`:

```json
{
  "mcpServers": {
    "mysql": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-mysql",
        "mysql://username:password@localhost:3306/database_name"
      ]
    }
  }
}
```

**连接字符串格式：**
```
mysql://[用户名]:[密码]@[主机]:[端口]/[数据库名]?[参数]

示例：
mysql://root:mypassword@localhost:3306/ecommerce
mysql://app_user:secret123@192.168.1.100:3306/orders_db
mysql://user:pass@db.example.com:3306/prod?charset=utf8mb4
```

**使用环境变量（更安全）：**

```json
{
  "mcpServers": {
    "mysql": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-mysql"
      ],
      "env": {
        "MYSQL_CONNECTION_STRING": "mysql://username:password@localhost:3306/database"
      }
    }
  }
}
```

然后在 `~/.bashrc` 或 `~/.zshrc` 中设置：
```bash
export MYSQL_CONNECTION_STRING="mysql://root:mypassword@localhost:3306/mydb"
```

3. **验证连接**

```bash
# 启动 Claude Code
claude

用户: 检查 MySQL 连接

Claude: [使用 MySQL MCP]
✓ 已连接到 MySQL 数据库
数据库: ecommerce
主机: localhost:3306
用户: root
字符集: utf8mb4

用户: 列出所有表

Claude:
数据库 ecommerce 包含以下表：
1. users (用户表)
2. orders (订单表)
3. products (商品表)
4. order_items (订单明细表)
5. categories (分类表)
...
```

**第二步：基本使用**

**1. 数据查询**

```bash
用户: 查询最近 7 天的订单统计

Claude: [使用 MySQL MCP]
SELECT
  DATE(created_at) as date,
  COUNT(*) as order_count,
  SUM(total_amount) as total_amount
FROM orders
WHERE created_at >= DATE_SUB(NOW(), INTERVAL 7 DAY)
GROUP BY DATE(created_at)
ORDER BY date DESC;

结果：
| 日期       | 订单数 | 总金额    |
|-----------|--------|----------|
| 2026-01-30 | 145    | 45230.50 |
| 2026-01-29 | 132    | 39876.00 |
| 2026-01-28 | 128    | 38456.80 |
| 2026-01-27 | 156    | 48923.20 |
| 2026-01-26 | 143    | 42115.60 |
| 2026-01-25 | 89     | 26784.30 |
| 2026-01-24 | 92     | 27845.40 |

分析：
- 周末订单量较少（周六 89单，周日 92单）
- 周四达到峰值（156单）
- 总计 7天：885 单，总额 ¥269,231.80
```

**2. 表结构分析**

```bash
用户: 分析 orders 表的结构

Claude:
orders 表结构：

| 字段名 | 类型 | 允许NULL | 键 | 默认值 | 注释 |
|--------|------|---------|-----|--------|------|
| id | bigint(20) | NO | PRI | NULL | 订单ID |
| user_id | bigint(20) | NO | MUL | NULL | 用户ID |
| order_no | varchar(32) | NO | UNI | NULL | 订单号 |
| total_amount | decimal(10,2) | NO | | 0.00 | 总金额 |
| status | tinyint(4) | NO | MUL | 0 | 订单状态 |
| created_at | datetime | NO | MUL | NULL | 创建时间 |
| updated_at | datetime | NO | | NULL | 更新时间 |

索引：
- PRIMARY KEY (id)
- UNIQUE KEY idx_order_no (order_no)
- KEY idx_user_id (user_id)
- KEY idx_status (status)
- KEY idx_created_at (created_at)

建议：
✓ 索引配置合理
△ 考虑添加组合索引 (user_id, status) 以优化用户订单查询
```

**3. 性能分析**

```bash
用户: 分析这个查询的性能

SELECT o.*, u.username, u.email
FROM orders o
LEFT JOIN users u ON o.user_id = u.id
WHERE o.created_at >= '2026-01-01'
AND o.status = 1
ORDER BY o.created_at DESC
LIMIT 100;

Claude: [执行 EXPLAIN]

查询计划分析：
| id | type | table | key | rows | Extra |
|----|------|-------|-----|------|-------|
| 1 | range | o | idx_created_at | 2500 | Using where |
| 1 | eq_ref | u | PRIMARY | 1 | NULL |

性能评估：
✓ 使用了索引 idx_created_at
✓ users 表使用主键查询，效率高
△ 扫描行数 2500，如果数据量大可能较慢

优化建议：
1. 添加组合索引：CREATE INDEX idx_created_status ON orders(created_at, status)
2. 如果只需要部分用户信息，选择具体字段而非 o.*
3. 考虑添加缓存（Redis）缓存热门查询

优化后的查询：
SELECT o.id, o.order_no, o.total_amount, o.status, o.created_at,
       u.username, u.email
FROM orders o
LEFT JOIN users u ON o.user_id = u.id
WHERE o.created_at >= '2026-01-01'
AND o.status = 1
ORDER BY o.created_at DESC
LIMIT 100;

预计性能提升: 40-60%
```

**4. 数据迁移脚本生成**

```bash
用户: 需要在 users 表添加 phone 字段，生成迁移脚本

Claude:
生成数据库迁移脚本：

-- V1.2.0__add_phone_to_users.sql

-- 添加手机号字段
ALTER TABLE users
ADD COLUMN phone VARCHAR(20) COMMENT '手机号' AFTER email;

-- 添加索引（手机号可能用于登录）
CREATE INDEX idx_phone ON users(phone);

-- 回滚脚本（如需要）
-- ALTER TABLE users DROP COLUMN phone;
-- DROP INDEX idx_phone ON users;

执行建议：
1. 在测试环境先执行验证
2. 建议在业务低峰期执行
3. 添加字段不会锁表（InnoDB），安全
4. 执行前备份数据库

需要我执行这个迁移吗？(yes/no)
```

**5. 生成测试数据**

```bash
用户: 为 products 表生成 50 条测试数据

Claude:
生成测试数据脚本：

INSERT INTO products (name, price, stock, category_id, description, created_at, updated_at)
VALUES
('iPhone 15 Pro', 7999.00, 100, 1, '苹果旗舰手机，A17 Pro芯片', NOW(), NOW()),
('MacBook Pro 14寸', 14999.00, 50, 1, '专业笔记本电脑，M3 Pro芯片', NOW(), NOW()),
('AirPods Pro 2', 1899.00, 200, 2, '主动降噪耳机', NOW(), NOW()),
...
(共 50 条记录)

特点：
- 包含多种价格区间（100-20000元）
- 涵盖不同类别
- 库存量随机（10-500）
- 自动生成时间戳

需要我执行插入吗？
```

**第三步：高级应用**

**1. 多数据库切换**

```json
{
  "mcpServers": {
    "mysql-dev": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-mysql", "mysql://root:pwd@localhost:3306/dev_db"]
    },
    "mysql-test": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-mysql", "mysql://root:pwd@localhost:3306/test_db"]
    },
    "mysql-prod-readonly": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-mysql", "mysql://readonly:pwd@prod.example.com:3306/prod_db"]
    }
  }
}
```

使用：
```bash
用户: 使用 mysql-dev 查询用户数量
用户: 使用 mysql-prod-readonly 查询生产环境的订单统计
```

**2. 数据对比**

```bash
用户: 对比开发环境和测试环境的 users 表结构差异

Claude:
[对比 mysql-dev 和 mysql-test]

结构差异：
开发环境独有：
  - phone VARCHAR(20) (新增字段)
  - idx_phone (新增索引)

测试环境独有：
  - 无

字段定义差异：
  - email: 开发环境 VARCHAR(100)，测试环境 VARCHAR(50)

建议：
需要将开发环境的变更同步到测试环境
```

**常见应用场景**

1. **数据分析和报表**
   - 销售统计
   - 用户行为分析
   - 性能监控数据查询

2. **性能问题排查**
   - 慢查询分析（EXPLAIN）
   - 索引优化建议
   - 查询重写

3. **数据库维护**
   - 表结构变更
   - 索引管理
   - 数据清理

4. **开发辅助**
   - 生成实体类（Entity）
   - 生成 MyBatis Mapper
   - 生成测试数据

5. **数据迁移**
   - 生成迁移脚本
   - 数据转换
   - 环境同步

#### 7.3.2 MongoDB MCP 详细配置和使用

MongoDB MCP 允许 Claude Code 连接和操作 MongoDB 数据库，适合处理文档型数据。

**第一步：安装配置**

1. **安装 MongoDB MCP Server**

```bash
# MongoDB MCP Server（社区版）
npm install -g @modelcontextprotocol/server-mongodb
```

2. **配置 MCP 服务器**

编辑 `~/.claude/mcp-config.json`:

```json
{
  "mcpServers": {
    "mongodb": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-mongodb",
        "mongodb://username:password@localhost:27017/database_name"
      ]
    }
  }
}
```

**连接字符串格式：**
```
mongodb://[用户名]:[密码]@[主机]:[端口]/[数据库]?[选项]

示例：
mongodb://localhost:27017/myapp
mongodb://admin:password@localhost:27017/myapp?authSource=admin
mongodb://user:pass@mongo1.example.com:27017,mongo2.example.com:27017/myapp?replicaSet=myReplicaSet
mongodb+srv://username:password@cluster0.mongodb.net/myapp (MongoDB Atlas)
```

**使用环境变量：**

```json
{
  "mcpServers": {
    "mongodb": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-mongodb"],
      "env": {
        "MONGODB_URI": "mongodb://username:password@localhost:27017/database"
      }
    }
  }
}
```

3. **验证连接**

```bash
claude

用户: 检查 MongoDB 连接

Claude: [使用 MongoDB MCP]
✓ 已连接到 MongoDB
数据库: ecommerce
主机: localhost:27017
MongoDB 版本: 7.0.5

用户: 列出所有集合

Claude:
数据库 ecommerce 包含以下集合：
1. users (254 个文档)
2. products (1,823 个文档)
3. orders (5,647 个文档)
4. reviews (3,892 个文档)
5. sessions (128 个文档)
```

**第二步：基本使用**

**1. 文档查询**

```bash
用户: 查询最近购买的 10 个订单

Claude: [使用 MongoDB MCP]
db.orders.find()
  .sort({ createdAt: -1 })
  .limit(10)

结果：
[
  {
    "_id": ObjectId("65b8f2a3c4d5e6f7g8h9i0j1"),
    "orderNo": "ORD20260130001",
    "userId": ObjectId("65a1b2c3d4e5f6g7h8i9j0k1"),
    "items": [
      {
        "productId": ObjectId("659a8b7c6d5e4f3g2h1i0j9k"),
        "productName": "iPhone 15 Pro",
        "price": 7999.00,
        "quantity": 1
      }
    ],
    "totalAmount": 7999.00,
    "status": "paid",
    "createdAt": ISODate("2026-01-30T10:23:45.000Z"),
    "updatedAt": ISODate("2026-01-30T10:24:12.000Z")
  },
  ...
]

统计信息：
- 共查询到 10 条订单
- 时间范围: 2026-01-30 08:15 ~ 10:23
- 总金额: ¥125,847.00
```

**2. 聚合查询**

```bash
用户: 统计每个分类的商品数量和平均价格

Claude:
db.products.aggregate([
  {
    $group: {
      _id: "$categoryId",
      count: { $sum: 1 },
      avgPrice: { $avg: "$price" },
      minPrice: { $min: "$price" },
      maxPrice: { $max: "$price" }
    }
  },
  {
    $lookup: {
      from: "categories",
      localField: "_id",
      foreignField: "_id",
      as: "category"
    }
  },
  {
    $unwind: "$category"
  },
  {
    $project: {
      categoryName: "$category.name",
      count: 1,
      avgPrice: { $round: ["$avgPrice", 2] },
      minPrice: 1,
      maxPrice: 1
    }
  },
  {
    $sort: { count: -1 }
  }
])

结果：
| 分类     | 商品数 | 平均价格 | 最低价 | 最高价  |
|---------|--------|---------|-------|---------|
| 电子产品 | 456    | 3,245.60 | 99.00 | 15,999.00 |
| 服装鞋帽 | 382    | 289.50   | 39.00 | 1,299.00 |
| 图书音像 | 298    | 68.80    | 12.00 | 298.00 |
| 家居用品 | 234    | 456.30   | 25.00 | 3,599.00 |
| 食品饮料 | 189    | 45.20    | 5.00  | 299.00 |
```

**3. 文档结构分析**

```bash
用户: 分析 orders 集合的文档结构

Claude:
orders 集合文档结构分析：

【基本结构】
{
  _id: ObjectId,                 // MongoDB 自动生成的ID
  orderNo: String,               // 订单号（唯一）
  userId: ObjectId,              // 用户ID（引用 users 集合）
  items: Array[Object],          // 订单项数组
  totalAmount: Number,           // 总金额
  status: String,                // 订单状态
  shippingAddress: Object,       // 收货地址（嵌套文档）
  paymentInfo: Object,           // 支付信息（嵌套文档）
  createdAt: Date,               // 创建时间
  updatedAt: Date                // 更新时间
}

【items 子文档结构】
{
  productId: ObjectId,           // 商品ID
  productName: String,           // 商品名称（冗余存储）
  price: Number,                 // 购买时价格
  quantity: Number,              // 数量
  subtotal: Number               // 小计
}

【索引】
1. _id (默认)
2. orderNo (唯一索引)
3. userId (普通索引)
4. status (普通索引)
5. createdAt (普通索引)
6. { userId: 1, status: 1 } (组合索引)

【数据统计】
- 总文档数: 5,647
- 平均文档大小: 2.3 KB
- 总集合大小: 12.9 MB
- 索引大小: 856 KB
```

**4. 数据迁移和导入**

```bash
用户: 生成 50 条测试用户数据

Claude:
生成测试数据：

const testUsers = [
  {
    username: "user001",
    email: "user001@example.com",
    phone: "13800138001",
    profile: {
      nickname: "测试用户001",
      avatar: "https://example.com/avatars/001.jpg",
      gender: "male",
      birthday: new Date("1990-01-15")
    },
    address: [
      {
        province: "北京市",
        city: "北京市",
        district: "朝阳区",
        detail: "XX路XX号",
        isDefault: true
      }
    ],
    createdAt: new Date(),
    updatedAt: new Date()
  },
  // ... 49 more users
];

db.users.insertMany(testUsers);

特点：
- 真实的中国姓名、手机号
- 多样化的个人资料
- 每个用户1-3个收货地址
- 自动生成创建时间

需要我执行插入吗？
```

**5. 性能优化**

```bash
用户: 优化这个查询的性能

db.orders.find({
  userId: ObjectId("..."),
  status: "paid",
  createdAt: { $gte: ISODate("2026-01-01") }
}).sort({ createdAt: -1 })

Claude: [分析查询计划]

查询计划：
{
  "executionStats": {
    "nReturned": 45,
    "totalKeysExamined": 1258,
    "totalDocsExamined": 1258,
    "executionStages": {
      "stage": "SORT",
      "inputStage": {
        "stage": "FETCH",
        "inputStage": {
          "stage": "IXSCAN",
          "keyPattern": { "userId": 1 },
          "indexName": "userId_1"
        }
      }
    }
  }
}

问题分析：
⚠ 使用了 userId 索引，但需要扫描 1258 个文档
⚠ 在内存中进行排序（SORT stage）
⚠ 没有充分利用 status 和 createdAt 过滤条件

优化方案：
1. 创建组合索引（推荐）
db.orders.createIndex({
  userId: 1,
  status: 1,
  createdAt: -1
})

2. 使用索引后的查询计划：
  - 扫描文档数: 1258 → 45
  - 内存排序: 是 → 否
  - 执行时间: 125ms → 8ms

需要我创建这个索引吗？
```

**第三步：高级应用**

**1. 实时数据分析**

```bash
用户: 分析最近 24 小时的订单趋势

Claude:
db.orders.aggregate([
  {
    $match: {
      createdAt: {
        $gte: new Date(Date.now() - 24 * 60 * 60 * 1000)
      }
    }
  },
  {
    $group: {
      _id: {
        $dateToString: {
          format: "%Y-%m-%d %H:00",
          date: "$createdAt"
        }
      },
      count: { $sum: 1 },
      totalAmount: { $sum: "$totalAmount" },
      avgAmount: { $avg: "$totalAmount" }
    }
  },
  {
    $sort: { _id: 1 }
  }
])

结果（每小时统计）：
| 时间段      | 订单数 | 总金额    | 平均金额 |
|------------|-------|----------|---------|
| 2026-01-29 11:00 | 12    | 15,847.00 | 1,320.58 |
| 2026-01-29 12:00 | 23    | 28,956.00 | 1,259.39 |
| 2026-01-29 13:00 | 18    | 22,145.00 | 1,230.28 |
| ...              | ...   | ...       | ...      |
| 2026-01-30 10:00 | 15    | 19,234.00 | 1,282.27 |

高峰时段：14:00-16:00 (51单)
低峰时段：02:00-06:00 (8单)
```

**2. 数据清理**

```bash
用户: 清理 30 天前的临时会话数据

Claude:
db.sessions.deleteMany({
  createdAt: {
    $lt: new Date(Date.now() - 30 * 24 * 60 * 60 * 1000)
  },
  type: "temp"
})

预览将删除的数据：
- 符合条件的文档: 3,847 个
- 预计释放空间: ~12.5 MB

确认删除吗？(yes/no)

用户: yes

Claude:
删除完成：
✓ 已删除 3,847 个临时会话
✓ 释放空间 12.6 MB
✓ 剩余活跃会话: 128 个
```

**常见应用场景**

1. **文档型数据存储**
   - 用户配置、个人资料
   - 日志和事件数据
   - 内容管理系统

2. **实时分析**
   - 用户行为追踪
   - 实时报表统计
   - 聚合查询

3. **灵活的数据模型**
   - 动态字段
   - 嵌套文档
   - 数组字段

4. **开发辅助**
   - 生成 Mongoose Schema
   - 生成 Spring Data MongoDB Entity
   - 数据模型设计建议

**MySQL vs MongoDB 选择建议**

| 场景 | 推荐 | 原因 |
|------|------|------|
| 事务性数据 | MySQL | ACID 保证 |
| 结构化数据 | MySQL | 强类型约束 |
| 复杂关联查询 | MySQL | JOIN 支持好 |
| 文档型数据 | MongoDB | 灵活的 Schema |
| 大规模日志 | MongoDB | 写入性能高 |
| 实时分析 | MongoDB | 聚合管道强大 |
| 动态字段 | MongoDB | Schema-less |
| 金融数据 | MySQL | 事务保证 |

#### 7.3.2 GitHub/GitLab MCP

**场景**: 代码仓库管理和 PR 审查

```bash
用户: 查看我负责的所有待审查 PR

Claude: [使用 GitHub MCP]
找到 3 个待审查的 PR:

1. PR #234: feat: 添加订单导出功能
   - 作者: zhangsan
   - 变更: +245 -12
   - 状态: 等待审查

2. PR #235: fix: 修复库存并发问题
   - 作者: lisi
   - 变更: +67 -23
   - 状态: 等待审查

需要我帮你审查吗？

用户: 审查 PR #234

Claude: [自动拉取代码并分析]
代码审查结果：

✓ 代码风格符合规范
✓ 单元测试覆盖率 82%
⚠ 建议：ExcelExportService 应添加大文件限制
⚠ 建议：导出接口应添加权限校验
✗ 问题：缺少异常处理（L45-L67）

已生成审查意见并发布到 PR。
```

**用途**：
- 自动化 Code Review
- PR 创建和管理
- Issue 跟踪
- 代码统计分析

#### 7.3.3 Slack/Teams MCP

**场景**: 团队协作和通知

```bash
用户: 部署完成后通知团队

Claude: [使用 Slack MCP]
已发送消息到 #dev-team:

📦 部署通知
✓ 订单服务 v1.2.0 已部署到生产环境
✓ 部署时间: 2026-01-30 14:30
✓ 新功能: 订单导出、库存优化
✓ 回滚命令: ./scripts/rollback.sh v1.1.9

测试地址: https://api.example.com/orders
```

#### 7.3.4 Jira/Linear MCP

**场景**: 任务管理和进度跟踪

```bash
用户: 创建一个技术债务任务：优化订单查询性能

Claude: [使用 Jira MCP]
已创建任务 TECH-456:

标题: 优化订单查询性能
类型: 技术债务
优先级: 中
描述:
- 当前订单列表查询响应时间 >2s
- 需要添加数据库索引
- 考虑引入分页缓存
估算: 3 Story Points
指派: 未分配

链接: https://jira.example.com/browse/TECH-456
```

#### 7.3.5 Chrome DevTools MCP

**场景**: Web 应用测试、调试和自动化

Chrome DevTools MCP 允许 Claude Code 直接控制 Chrome 浏览器，进行网页测试、UI 验证、性能分析等操作。

**安装配置：**

```json
{
  "mcpServers": {
    "chrome-devtools": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-chrome-devtools"
      ]
    }
  }
}
```

**主要功能：**

1. **页面导航和交互**
```bash
用户: 打开我们的测试环境并登录

Claude: [使用 chrome-devtools MCP]
✓ 导航到 https://test.example.com
✓ 填写用户名: test@example.com
✓ 填写密码: ******
✓ 点击登录按钮
✓ 等待页面加载完成
✓ 已成功登录，当前页面: /dashboard
```

2. **截图和快照**
```bash
用户: 检查首页在不同屏幕尺寸下的显示效果

Claude:
正在测试不同屏幕尺寸...

Desktop (1920x1080):
✓ 截图已保存: desktop-homepage.png
✓ 布局正常，所有元素可见

Tablet (768x1024):
✓ 截图已保存: tablet-homepage.png
✓ 响应式布局正常

Mobile (375x667):
✓ 截图已保存: mobile-homepage.png
⚠ 发现问题：导航菜单被截断
```

3. **表单测试**
```bash
用户: 测试用户注册流程

Claude: [自动化测试注册流程]
1. 导航到注册页面
2. 填写表单：
   ✓ 用户名: testuser123
   ✓ 邮箱: test123@example.com
   ✓ 密码: Test@123456
   ✓ 确认密码: Test@123456
3. 点击提交
4. 验证结果：
   ✓ 注册成功
   ✓ 收到欢迎邮件（检查邮件内容）
   ✓ 自动跳转到首页
```

4. **性能分析**
```bash
用户: 分析首页的加载性能

Claude: [使用 Performance API]
性能分析报告：

【Core Web Vitals】
• LCP (Largest Contentful Paint): 2.1s (需要优化)
• FID (First Input Delay): 45ms (良好)
• CLS (Cumulative Layout Shift): 0.05 (良好)

【加载时间】
• DOMContentLoaded: 1.2s
• Load: 3.4s

【资源加载】
• JavaScript: 8 个文件，总计 450KB
  ⚠ vendor.js (320KB) 过大
• CSS: 3 个文件，总计 85KB
• 图片: 12 个，总计 2.1MB
  ⚠ hero-banner.jpg (1.2MB) 未压缩

【优化建议】
1. 对 vendor.js 进行代码分割
2. 压缩 hero-banner.jpg（推荐使用 WebP 格式）
3. 启用浏览器缓存
4. 使用 CDN 加速静态资源
```

5. **控制台日志监控**
```bash
用户: 监控页面是否有JavaScript错误

Claude:
正在监控控制台输出...

【发现 2 个错误】
1. TypeError: Cannot read property 'length' of undefined
   位置: app.js:234
   触发: 点击"加载更多"按钮时

2. Network Error: Failed to fetch
   URL: https://api.example.com/users
   状态码: 404
   触发: 页面加载时

【警告】
⚠ React deprecated method warning in UserList component
```

6. **网络请求监控**
```bash
用户: 检查API请求是否正常

Claude: [监控网络请求]
【API 请求监控】
GET /api/users
  ✓ 状态: 200 OK
  ✓ 响应时间: 245ms
  ✓ 数据量: 15KB

POST /api/orders
  ✗ 状态: 500 Internal Server Error
  ✗ 响应时间: 3200ms
  ✗ 错误信息: "Database connection timeout"

建议：
- 检查数据库连接配置
- 增加连接超时重试机制
```

7. **跨浏览器测试**
```bash
用户: 测试在不同浏览器中的兼容性

Claude:
正在测试浏览器兼容性...

Chrome 120:
  ✓ 功能正常
  ✓ 布局正常
  ✓ 性能良好

Firefox 121:
  ✓ 功能正常
  ⚠ CSS Grid 显示略有差异
  ✓ 性能可接受

Safari 17:
  ✗ localStorage 在隐私模式下失败
  ⚠ Date.parse() 行为不一致
  建议：使用 polyfill 或替代方案
```

**典型应用场景：**
- E2E 测试自动化
- UI/UX 验证
- 性能监控和优化
- Bug 重现和调试
- 可访问性检查
- SEO 分析

#### 7.3.6 自定义 MCP Server

**场景**: 连接内部系统

创建自定义 MCP Server（Python 示例）:

```python
# custom-mcp-server.py
from fastmcp import FastMCP

mcp = FastMCP("Internal Tools")

@mcp.tool()
def query_redis_cache(key: str) -> dict:
    """查询 Redis 缓存"""
    import redis
    r = redis.Redis(host='localhost', port=6379, db=0)
    value = r.get(key)
    return {
        "key": key,
        "value": value.decode() if value else None,
        "exists": value is not None
    }

@mcp.tool()
def clear_cache(pattern: str) -> dict:
    """清除匹配模式的缓存"""
    import redis
    r = redis.Redis(host='localhost', port=6379, db=0)
    keys = r.keys(pattern)
    deleted = r.delete(*keys) if keys else 0
    return {
        "pattern": pattern,
        "deleted_count": deleted
    }

if __name__ == "__main__":
    mcp.run()
```

配置到 `mcp-config.json`:

```json
{
  "mcpServers": {
    "internal-tools": {
      "command": "python",
      "args": ["/path/to/custom-mcp-server.py"]
    }
  }
}
```

使用：

```bash
用户: 查询订单缓存 order:12345

Claude: [使用 internal-tools MCP]
{
  "key": "order:12345",
  "value": "{\"id\":12345,\"status\":\"paid\",\"amount\":299.99}",
  "exists": true
}
```

### 7.4 MCP 最佳实践

1. **安全性**
   - 敏感信息（token、密码）使用环境变量
   - 限制 MCP Server 权限（只读 vs 读写）
   - 定期轮换访问凭证

2. **性能优化**
   - 缓存频繁查询的数据
   - 使用连接池
   - 设置合理的超时时间

3. **错误处理**
   - MCP Server 应返回清晰的错误信息
   - 实现重试机制
   - 监控 MCP 调用失败率

---

## 8. Skills 技能系统

### 8.1 什么是 Skills

Skills 是预定义的工作流程和知识模板，可以：
- 封装重复性任务
- 规范团队工作流
- 传承领域知识
- 提升执行效率

### 8.2 内置 Skills 示例

#### 8.2.1 `/commit` - 智能提交

```bash
# 使用 /commit 自动生成提交信息
/commit

Claude:
检测到以下变更：
- 新增 OrderExportController.java
- 修改 OrderService.java
- 新增测试用例 OrderExportTest.java

生成提交信息：
feat(order): 添加订单导出功能

- 新增 Excel 导出接口 POST /api/orders/export
- 支持按条件筛选导出
- 异步处理大批量导出请求
- 单元测试覆盖率 85%

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>

是否确认提交？
```

#### 8.2.2 `/review-pr` - PR 审查

```bash
/review-pr 234

Claude:
正在审查 PR #234...

【代码质量】 ⭐⭐⭐⭐☆
✓ 代码风格一致
✓ 命名清晰
✓ 注释充分
△ 部分方法过长，建议拆分

【测试覆盖】 ⭐⭐⭐⭐☆
✓ 单元测试覆盖率 82%
△ 缺少集成测试
△ 缺少异常场景测试

【安全性】 ⭐⭐⭐☆☆
⚠ 文件导出无大小限制，存在 DoS 风险
⚠ 缺少权限校验

【性能】 ⭐⭐⭐⭐☆
✓ 查询使用了索引
△ 建议添加分页限制

【建议】
1. 添加文件大小限制 (建议 10MB)
2. 添加权限注解 @RequiresPermission("order:export")
3. 大量数据导出应使用异步任务

整体评分: 3.5/5 - 建议修改后合并
```

### 8.3 创建自定义 Skills

#### 8.3.1 团队开发规范 Skill

创建 `~/.claude/skills/team-dev-standard.md`:

```markdown
---
name: team-dev-standard
description: 团队开发规范检查
---

# 团队开发规范

检查代码是否符合团队规范：

## 后端 Java 规范
1. Controller 方法必须添加 @ApiOperation 注解
2. 所有 public 方法必须有 JavaDoc
3. 异常使用 BusinessException
4. 返回值统一使用 Result<T>
5. 日志级别使用规范：
   - ERROR: 系统错误
   - WARN: 业务异常
   - INFO: 关键业务流程
   - DEBUG: 调试信息

## 前端 Vue 规范
1. 组件必须有 name 属性
2. Props 必须定义类型和默认值
3. 大型组件拆分（< 300 行）
4. API 调用使用 async/await
5. 表单验证使用 rules

## 数据库规范
1. 表必须有主键 id
2. 必须有 created_at, updated_at
3. 必须有逻辑删除字段 deleted
4. 索引命名: idx_字段名
5. 外键命名: fk_表名_字段名

## Git 规范
1. 提交信息格式: type(scope): description
2. 类型: feat, fix, refactor, docs, test, chore
3. 每次提交只做一件事
4. 提交前必须通过 lint 检查

请按照以上规范检查代码并生成报告。
```

使用：

```bash
/team-dev-standard

Claude:
正在检查代码规范...

【后端规范检查】
✓ Controller 注解完整
✗ UserService.updateUser() 缺少 JavaDoc
✓ 异常处理规范
✗ OrderController.export() 返回类型应为 Result<T>

【前端规范检查】
✓ 组件命名规范
✗ UserForm.vue props 未定义默认值
✓ API 调用使用 async/await
△ OrderList.vue 组件过长 (456 行)

【数据库规范检查】
✓ 表结构符合规范
✗ order_item 表缺少索引

发现 5 处不符合规范，是否自动修复？
```

#### 8.3.2 自动化测试 Skill

创建 `~/.claude/skills/auto-test.md`:

```markdown
---
name: auto-test
description: 自动生成单元测试和集成测试
---

# 自动化测试生成

为指定的类或模块生成完整的测试用例：

## 单元测试
- 测试所有 public 方法
- 覆盖正常场景和异常场景
- Mock 外部依赖
- 使用 JUnit 5 + Mockito (Java) 或 Jest (JavaScript)

## 测试用例设计
1. 边界值测试
2. 空值/null 测试
3. 异常场景测试
4. 并发测试（如适用）

## 集成测试
- 使用 @SpringBootTest (Java) 或 测试容器
- 测试完整业务流程
- 验证数据库操作
- 验证缓存行为

目标覆盖率: 80%+
```

使用：

```bash
/auto-test OrderService

Claude:
正在为 OrderService 生成测试用例...

✓ 生成 OrderServiceTest.java
  - testCreateOrder_Success()
  - testCreateOrder_InsufficientStock()
  - testCreateOrder_InvalidUser()
  - testQueryOrders_WithPagination()
  - testCancelOrder_Success()
  - testCancelOrder_AlreadyCancelled()

✓ 生成 OrderServiceIntegrationTest.java
  - testCreateOrderFlow()
  - testOrderPaymentFlow()
  - testConcurrentOrderCreation()

测试覆盖率: 87%
运行测试... ✓ 全部通过 (15/15)
```

#### 8.3.3 部署流程 Skill

创建 `~/.claude/skills/deploy.md`:

```markdown
---
name: deploy
description: 标准化部署流程
arguments:
  - name: environment
    description: 目标环境 (dev/test/prod)
    required: true
  - name: version
    description: 版本号
    required: false
---

# 部署流程

## 部署前检查
1. 代码已合并到对应分支
2. 所有测试通过
3. Code Review 已完成
4. 数据库变更已准备
5. 配置文件已更新

## 部署步骤
1. 备份当前版本
2. 构建 Docker 镜像
3. 推送到镜像仓库
4. 更新 Kubernetes 配置
5. 执行滚动更新
6. 健康检查
7. 通知团队

## 回滚计划
- 保留最近 3 个版本
- 快速回滚命令
- 回滚验证

## 通知
- Slack 通知
- 更新部署文档
- 记录部署日志
```

使用：

```bash
/deploy test v1.2.0

Claude:
开始部署到测试环境...

[1/7] 部署前检查
✓ 代码已合并到 test 分支
✓ 测试通过 (156/156)
✓ PR #234 已审查通过
✓ 数据库迁移脚本已准备

[2/7] 备份当前版本
✓ 已备份 v1.1.9 到 /backup/v1.1.9

[3/7] 构建镜像
✓ 构建 order-service:v1.2.0
✓ 镜像大小: 245MB

[4/7] 推送镜像
✓ 推送到 registry.example.com/order-service:v1.2.0

[5/7] 更新配置
✓ 更新 deployment.yaml
✓ 应用配置到 k8s 集群

[6/7] 滚动更新
✓ Pod order-service-1 已更新
✓ Pod order-service-2 已更新
✓ Pod order-service-3 已更新

[7/7] 健康检查
✓ /health 端点正常
✓ /metrics 端点正常
✓ 数据库连接正常

✅ 部署成功！
已发送通知到 Slack #deployments
部署文档: https://wiki.example.com/deploy/v1.2.0
```

### 8.4 Skills 管理

```bash
# 列出所有可用 Skills
/skills

# 查看 Skill 详情
/skills show team-dev-standard

# 编辑 Skill
/skills edit auto-test

# 删除 Skill
/skills delete old-skill
```

---

## 9. 全自动化开发流程

### 9.1 完整开发流程示例

从需求到上线的全自动化流程：

```bash
claude

用户: 我要开发一个用户积分功能，包括：
1. 用户签到获得积分
2. 积分兑换商品
3. 积分明细查询
要求包含完整的测试、文档和部署

Claude: [进入计划模式]
```

#### 9.1.1 需求分析与设计

```bash
Claude:
【需求分析】
1. 功能模块
   - 签到模块
   - 积分管理
   - 商品兑换
   - 明细查询

2. 数据模型
   - user_points (用户积分表)
   - point_records (积分明细表)
   - exchange_goods (兑换商品表)
   - exchange_orders (兑换订单表)

3. API 设计
   POST /api/points/checkin - 签到
   POST /api/points/exchange - 兑换
   GET  /api/points/records - 明细
   GET  /api/points/goods - 商品列表

确认设计？
```

#### 9.1.2 自动生成代码

```bash
用户: 确认

Claude:
[Phase 1: 数据库设计]
✓ 生成数据库迁移脚本
✓ 创建表结构
✓ 添加索引

[Phase 2: 后端代码]
✓ Entity: UserPoints, PointRecord, ExchangeGoods
✓ Mapper: 对应的 MyBatis Mapper
✓ Service: PointService, ExchangeService
✓ Controller: PointController
✓ DTO: PointDTO, ExchangeDTO

[Phase 3: 前端代码]
✓ API: points.ts
✓ Views: PointsCenter.vue, ExchangeMall.vue
✓ Components: PointsRecord.vue
✓ Store: points.ts

代码生成完成！
```

#### 9.1.3 自动生成测试

```bash
Claude:
[Phase 4: 测试代码]
✓ 单元测试
  - PointServiceTest.java (12 个测试用例)
  - ExchangeServiceTest.java (10 个测试用例)

✓ 集成测试
  - PointsIntegrationTest.java (6 个测试场景)

✓ 前端测试
  - PointsCenter.spec.ts (8 个测试用例)

运行测试...
✓ 后端测试 通过 (28/28)
✓ 前端测试 通过 (8/8)
测试覆盖率: 89%
```

#### 9.1.4 自动构建

```bash
Claude:
[Phase 5: 构建]
✓ Maven 打包后端服务
✓ Vite 构建前端资源
✓ Docker 镜像构建
  - points-service:v1.0.0 (238MB)
✓ 推送到镜像仓库

构建成功！
```

#### 9.1.5 自动生成文档

```bash
Claude:
[Phase 6: 文档生成]
✓ API 文档 (Swagger)
✓ 数据库设计文档
✓ 部署手册
✓ 用户使用手册

文档地址:
- API: http://localhost:8080/swagger-ui.html
- 文档: ./docs/points-feature.md
```

#### 9.1.6 自动部署到测试环境

```bash
Claude:
[Phase 7: 部署到测试环境]
✓ 执行数据库迁移
✓ 更新 Kubernetes 配置
✓ 滚动更新服务
✓ 健康检查通过

测试环境部署成功！
URL: https://test-api.example.com/points
```

#### 9.1.7 创建 Pull Request (GitHub)

```bash
Claude:
[Phase 8: 提交代码]
✓ 提交代码到 feature/user-points 分支
✓ 推送到远程仓库

创建 Pull Request...
✓ PR #245 已创建

标题: feat(points): 用户积分功能
描述:
## 功能概述
实现用户积分系统，包括签到、兑换、明细查询

## 变更内容
- 新增积分相关表结构
- 实现签到、兑换 API
- 前端积分中心页面
- 完整的单元测试和集成测试

## 测试
- ✓ 单元测试覆盖率 89%
- ✓ 集成测试通过
- ✓ 测试环境验证通过

## 部署
已部署到测试环境: https://test-api.example.com/points

PR 链接: https://github.com/example/project/pull/245
```

#### 9.1.8 创建 Pull Request (Gitee)

对于 Gitee 平台，流程类似：

```bash
Claude: [使用 Gitee API 或 MCP]
✓ 创建 Pull Request 到 Gitee

标题: feat(points): 用户积分功能
目标分支: develop
源分支: feature/user-points

已添加审查人: @team-lead
已添加标签: enhancement, backend, frontend

PR 链接: https://gitee.com/example/project/pulls/245

需要我通知团队吗？
```

### 9.2 自动化 Code Review

```bash
# PR 创建后，自动审查
Claude:
收到 PR #245 创建通知，开始自动审查...

【代码质量检查】
✓ 代码风格符合规范
✓ 无 ESLint/Checkstyle 警告
✓ 无安全漏洞

【架构审查】
✓ 遵循现有架构模式
✓ 模块职责清晰
△ 建议: ExchangeService 可进一步拆分

【测试审查】
✓ 单元测试覆盖率 89% (>80%)
✓ 关键路径有集成测试
△ 建议: 添加并发场景测试

【文档审查】
✓ API 文档完整
✓ 代码注释充分
✓ README 已更新

总体评分: 4.5/5 ⭐⭐⭐⭐☆

审查意见已发布到 PR。
```

### 9.3 自动化发布流程

#### 9.3.1 版本管理

```bash
用户: PR 已合并，准备发布 v1.3.0

Claude:
[版本发布流程]

[1/6] 版本准备
✓ 更新 pom.xml 版本号
✓ 更新 package.json 版本号
✓ 生成 CHANGELOG.md

[2/6] 构建生产版本
✓ Maven clean package -P prod
✓ Vite build --mode production
✓ 运行生产环境测试

[3/6] 创建 Git Tag
✓ 创建 tag v1.3.0
✓ 推送到远程仓库

[4/6] 构建生产镜像
✓ 构建 points-service:v1.3.0
✓ 扫描镜像安全漏洞: ✓ 无高危漏洞
✓ 推送到生产镜像仓库

[5/6] 创建 GitHub Release
✓ Release v1.3.0 已创建
✓ 发布说明已生成
✓ 附件: points-service-v1.3.0.jar

[6/6] 通知
✓ Slack 通知已发送
✓ Jira ticket 已更新
✓ 部署文档已准备

Release: https://github.com/example/project/releases/tag/v1.3.0
```

#### 9.3.2 生产环境部署

```bash
用户: 部署到生产环境

Claude:
⚠ 生产环境部署需要额外确认

部署信息:
- 版本: v1.3.0
- 环境: production
- 影响: 积分模块
- 回滚版本: v1.2.5

数据库变更:
- 新增表: user_points, point_records, exchange_goods, exchange_orders
- 无数据迁移

预计影响:
- 服务重启时间: ~30s
- 预计流量影响: 无（新功能）

是否继续？(yes/no)

用户: yes

Claude:
[生产环境部署]

[1/8] 备份
✓ 数据库备份完成
✓ 配置文件备份完成
✓ 当前版本快照已保存

[2/8] 数据库变更
✓ 执行迁移脚本 V1.3.0__points.sql
✓ 验证表结构
✓ 创建索引

[3/8] 灰度发布 (10%)
✓ 更新 1/10 Pod
✓ 等待 60s...
✓ 健康检查通过
✓ 错误率监控: 0%

[4/8] 灰度扩大 (50%)
✓ 更新 5/10 Pod
✓ 监控 QPS、响应时间、错误率
✓ 各项指标正常

[5/8] 全量发布
✓ 更新所有 Pod
✓ 滚动重启完成

[6/8] 验证
✓ 健康检查: 10/10 Pod 健康
✓ API 测试通过
✓ 数据库连接正常
✓ Redis 连接正常

[7/8] 监控
✓ 设置告警规则
✓ 配置监控面板

[8/8] 通知
✓ 发送部署成功通知
✓ 更新部署记录

✅ 生产环境部署成功！

监控面板: https://grafana.example.com/points-service
回滚命令: kubectl rollout undo deployment/points-service
```

### 9.4 持续集成自动化

#### 9.4.1 配置 CI/CD Pipeline

```bash
用户: 配置 GitHub Actions CI/CD

Claude:
正在生成 .github/workflows/ci.yml...

✓ 已创建 CI Pipeline:
  - 触发: Push 到任意分支, PR
  - 步骤: Lint → Test → Build → Security Scan

✓ 已创建 CD Pipeline (deploy.yml):
  - 触发: Push tag v*
  - 步骤: Build → Push Image → Deploy to K8s → Notify

主要配置:
- Java 17
- Node.js 20
- MySQL 8.0 (服务容器)
- Redis 7.0 (服务容器)
- SonarQube 代码质量检查
- Trivy 镜像安全扫描

文件已创建: .github/workflows/{ci.yml, deploy.yml}
```

#### 9.4.2 自动化质量门禁

```bash
Claude:
配置 SonarQube 质量门禁:

质量要求:
✓ 代码覆盖率 ≥ 80%
✓ 重复代码率 ≤ 3%
✓ 无阻断性问题
✓ 无严重安全漏洞
✓ 技术债务 ≤ 1天

质量门禁已集成到 CI Pipeline
PR 合并前必须通过质量检查
```

---

## 10. 权限管理与安全

### 10.1 权限系统概述

Claude Code 提供细粒度的权限控制，确保安全性：

- **文件系统权限**: 控制可访问的目录
- **命令执行权限**: 控制可执行的命令
- **网络权限**: 控制外部 API 访问
- **MCP 权限**: 控制 MCP Server 访问

### 10.2 权限配置

#### 10.2.1 全局权限配置

编辑 `~/.claude/config.json`:

```json
{
  "permissions": {
    "filesystem": {
      "allowedPaths": [
        "/Users/username/projects",
        "/Users/username/work"
      ],
      "deniedPaths": [
        "/Users/username/.ssh",
        "/Users/username/.aws"
      ]
    },
    "commands": {
      "allowedCommands": [
        "git",
        "npm",
        "mvn",
        "docker"
      ],
      "dangerousCommands": {
        "requireConfirmation": [
          "rm -rf",
          "git push --force",
          "docker system prune"
        ]
      }
    },
    "network": {
      "allowedDomains": [
        "github.com",
        "api.example.com"
      ],
      "blockPrivateIPs": true
    }
  }
}
```

#### 10.2.2 项目级权限

在项目根目录创建 `.claude/permissions.json`:

```json
{
  "filesystem": {
    "readOnly": [
      "production-config/"
    ],
    "noAccess": [
      ".env.production",
      "secrets/"
    ]
  },
  "commands": {
    "allowed": [
      "npm test",
      "mvn clean install",
      "git status"
    ],
    "denied": [
      "git push origin master",
      "kubectl delete"
    ]
  }
}
```

### 10.3 敏感操作确认

某些操作需要用户明确确认：

```bash
Claude:
我需要执行以下命令:
  git push --force origin feature-branch

⚠ 这是一个危险操作，可能覆盖远程历史

是否继续？(yes/no)

用户: yes

Claude: ✓ 已执行 git push --force
```

### 10.4 审计日志

Claude Code 记录所有操作日志：

```bash
# 查看审计日志
cat ~/.claude/audit.log

[2026-01-30 14:23:15] READ /project/src/UserService.java
[2026-01-30 14:23:45] WRITE /project/src/UserService.java
[2026-01-30 14:24:10] EXEC git commit -m "feat: add user points"
[2026-01-30 14:24:30] MCP mysql QUERY SELECT * FROM users
[2026-01-30 14:25:00] EXEC git push origin feature/points
```

### 10.5 敏感信息处理

#### 10.5.1 自动检测敏感信息

```bash
Claude:
⚠ 检测到疑似敏感信息:

文件: application-prod.yml
行号: 15
内容: password: mySecretPassword123

建议:
1. 使用环境变量代替硬编码密码
2. 使用密钥管理服务 (如 AWS Secrets Manager)
3. 添加到 .gitignore

是否需要我帮你修复？
```

#### 10.5.2 环境变量管理

```bash
用户: 帮我配置数据库连接，但不要硬编码密码

Claude:
✓ 修改 application.yml:
```yaml
spring:
  datasource:
    url: jdbc:mysql://${DB_HOST:localhost}:${DB_PORT:3306}/${DB_NAME:mydb}
    username: ${DB_USERNAME}
    password: ${DB_PASSWORD}
```

✓ 创建 .env.example (提交到 Git):
```
DB_HOST=localhost
DB_PORT=3306
DB_NAME=mydb
DB_USERNAME=your_username
DB_PASSWORD=your_password
```

✓ 更新 .gitignore:
```
.env
.env.local
.env.*.local
```

✓ 创建 README 说明:
```markdown
## 环境变量配置
复制 .env.example 到 .env 并填写实际值
```

### 10.6 团队协作的权限最佳实践

#### 10.6.1 只读模式

适合学习和代码审查：

```bash
claude --read-only

# 此模式下：
# ✓ 可以读取文件
# ✓ 可以分析代码
# ✗ 不能修改文件
# ✗ 不能执行写操作命令
```

#### 10.6.2 沙箱模式

适合实验性操作：

```bash
claude --sandbox

# 此模式下：
# ✓ 所有操作在临时目录
# ✓ 不影响原始文件
# ✓ 退出后自动清理
```

#### 10.6.3 审批工作流

在团队环境中，配置审批流程：

```json
{
  "approvalRequired": {
    "filePatterns": [
      "*.production.yml",
      "Dockerfile",
      ".github/workflows/*"
    ],
    "commands": [
      "git push origin master",
      "kubectl apply",
      "npm publish"
    ],
    "approvers": [
      "tech-lead@example.com",
      "devops@example.com"
    ]
  }
}
```

---

## 11. 最佳实践与进阶技巧

### 11.1 提高效率的技巧

#### 11.1.1 使用快捷键

```bash
# VS Code 中
Cmd+K, Cmd+C - 快速注释解释
Cmd+K, Cmd+R - 快速重构
Cmd+K, Cmd+T - 生成测试用例
Cmd+K, Cmd+D - 生成文档
```

#### 11.1.2 批量操作

```bash
用户: 为所有 Service 类添加日志

Claude:
找到 15 个 Service 类:
- UserService.java
- OrderService.java
- ProductService.java
- ... (12 more)

批量添加日志:
✓ 导入 SLF4J Logger
✓ 添加 Logger 实例
✓ 在关键方法添加日志语句

已处理 15 个文件
```

#### 11.1.3 模板和代码片段

```bash
用户: 创建一个标准的 Controller 模板

Claude:
✓ 已创建模板 ~/.claude/templates/controller.java

使用方式:
  claude template controller --name=Product

模板内容:
- 标准 CRUD 端点
- 统一异常处理
- Swagger 注解
- 参数验证
- 日志记录
```

### 11.2 代码质量提升

#### 11.2.1 自动重构

```bash
用户: 重构这个类，消除代码坏味道

Claude:
识别到以下问题:
1. 方法过长 (updateOrder: 150 行)
2. 重复代码 (价格计算逻辑重复 3 次)
3. 过深的嵌套 (最深 6 层)
4. 魔法数字 (多处硬编码数值)

重构方案:
1. 提取方法 (拆分 updateOrder)
2. 提取公共方法 (PriceCalculator.calculate)
3. 早返回模式 (减少嵌套)
4. 提取常量 (定义 Constants 类)

[执行重构]
✓ 代码行数: 450 → 320
✓ 圈复杂度: 28 → 12
✓ 可维护性指数: 65 → 82
```

#### 11.2.2 性能优化

```bash
用户: 优化这个查询方法的性能

Claude:
分析当前实现:
- 执行了 N+1 查询
- 未使用索引
- 每次都查数据库（无缓存）

优化方案:
1. 使用 JOIN 替代 N+1 查询
2. 添加数据库索引
3. 添加 Redis 缓存（热点数据）
4. 使用分页限制结果集

[应用优化]
性能提升:
- 查询时间: 2.3s → 45ms (98% ↓)
- 数据库查询: 156 次 → 1 次
- CPU 使用率: 75% → 12%
```

### 11.3 团队协作

#### 11.3.1 知识分享

```bash
用户: 为新人准备项目入门文档

Claude:
生成项目入门指南:

✓ 架构概述图
✓ 模块职责说明
✓ 开发环境搭建步骤
✓ 常见问题 FAQ
✓ 代码规范检查清单
✓ 第一个 PR 指南

文档已保存: docs/onboarding.md
```

#### 11.3.2 技术债务管理

```bash
用户: 分析项目中的技术债务

Claude:
技术债务分析报告:

【高优先级】
1. 订单服务缺少分布式事务 (影响: 严重)
2. 用户密码存储未加密 (影响: 安全)
3. 日志未统一收集 (影响: 可观测性)

【中优先级】
1. 单元测试覆盖率不足 (当前: 45%, 目标: 80%)
2. API 文档过时
3. 配置管理混乱

【低优先级】
1. 代码风格不一致
2. 注释不充分
3. 依赖版本过旧

建议:
- 本周解决高优先级问题
- 本月解决中优先级问题
- 下季度处理低优先级问题

已创建 Jira tickets (TECH-456 到 TECH-464)
```

### 11.4 持续学习

#### 11.4.1 探索新技术

```bash
用户: 我想学习 Spring Cloud Alibaba，帮我创建一个示例项目

Claude:
创建 Spring Cloud Alibaba 学习项目:

✓ 搭建基础框架
  - Nacos 服务注册与发现
  - Sentinel 流量控制
  - Seata 分布式事务
  - RocketMQ 消息队列

✓ 创建示例服务
  - user-service (用户服务)
  - order-service (订单服务)
  - gateway (网关)

✓ 配置 Docker Compose 一键启动环境

✓ 编写学习文档
  - 核心概念讲解
  - 配置说明
  - 实战示例
  - 常见问题

项目已创建: ./spring-cloud-alibaba-demo/
启动命令: docker-compose up -d && mvn spring-boot:run
```

#### 11.4.2 代码审查学习

```bash
用户: 审查这个开源项目的代码，教我优秀的实践

Claude:
代码审查学习报告:

【优秀实践】
1. 异常处理模式
   - 使用自定义异常层次结构
   - 全局异常处理器
   - 详细的错误码设计

   示例代码: [展示代码]
   学习要点: ...

2. 缓存策略
   - 多级缓存（本地 + Redis）
   - 缓存预热机制
   - 缓存一致性保证

   示例代码: [展示代码]
   学习要点: ...

3. 测试策略
   - 分层测试（单元/集成/端到端）
   - 测试数据工厂模式
   - 测试容器使用

   示例代码: [展示代码]
   学习要点: ...

已保存学习笔记: docs/learning-notes.md
```

### 11.5 故障排查

#### 11.5.1 日志分析

```bash
用户: 分析最近 1 小时的错误日志

Claude:
日志分析结果:

【错误统计】
- 总错误数: 1,245
- 错误类型: 8 种
- 影响用户: 234

【Top 3 错误】
1. NullPointerException (56%)
   - 位置: OrderService.calculatePrice:156
   - 频率: 每分钟 12 次
   - 影响: 订单创建失败
   - 原因: 商品信息查询返回 null
   - 修复建议: 添加空值检查

2. TimeoutException (28%)
   - 位置: PaymentClient.pay:45
   - 频率: 每分钟 6 次
   - 影响: 支付超时
   - 原因: 第三方支付接口响应慢
   - 修复建议: 增加超时时间或添加重试

3. DatabaseException (12%)
   - 位置: UserMapper.updateUser:23
   - 频率: 每 5 分钟 1 次
   - 影响: 用户信息更新失败
   - 原因: 数据库连接池耗尽
   - 修复建议: 增加连接池大小

需要我创建 Bug Ticket 吗？
```

#### 11.5.2 性能诊断

```bash
用户: 为什么 API 响应这么慢？

Claude:
性能诊断:

【请求分析】
接口: POST /api/orders
平均响应时间: 3.2s

【耗时分解】
1. 数据库查询: 2.1s (66%)
   - 商品信息查询: 1.8s ⚠
   - 用户信息查询: 0.3s

2. 业务逻辑: 0.8s (25%)
   - 价格计算: 0.5s
   - 库存检查: 0.3s

3. 网络 I/O: 0.3s (9%)

【问题诊断】
⚠ 商品信息查询慢的原因:
- 查询了 1000+ 条记录
- 未使用索引（全表扫描）
- 查询了不必要的字段

【优化方案】
1. 立即可做:
   - 添加 WHERE 条件限制结果
   - 只查询需要的字段

2. 短期优化:
   - 添加数据库索引
   - 使用 Redis 缓存热门商品

3. 长期优化:
   - 考虑读写分离
   - 引入 Elasticsearch

预期提升: 3.2s → 150ms

需要我执行优化吗？
```

---

## 总结

使用 Claude Code 可以显著提升开发效率：

### 核心价值
1. **自动化重复工作**: 代码生成、测试、文档
2. **提升代码质量**: 自动审查、重构、优化
3. **加速学习曲线**: 快速理解新项目和技术
4. **规范团队协作**: 通过 Skills 统一工作流
5. **全流程覆盖**: 从需求到上线的完整自动化

### 关键能力
- **命令行与 VS Code 无缝集成**
- **计划模式保证复杂任务执行质量**
- **MCP 连接外部系统和工具**
- **Skills 封装团队知识和流程**
- **细粒度权限控制保证安全**

### 适用场景
- ✅ 日常开发任务
- ✅ 代码审查和重构
- ✅ 学习新技术栈
- ✅ 技术债务治理
- ✅ CI/CD 自动化
- ✅ 故障排查和性能优化

### 学习路径
1. **入门**: 安装配置，基础命令
2. **进阶**: 工作模式，新老项目开发
3. **高级**: MCP 集成，自定义 Skills
4. **专家**: 全流程自动化，团队知识沉淀

开始使用 Claude Code，让 AI 成为你的编程伙伴！

---

## 参考资源

- [Claude Code 官方文档](https://docs.anthropic.com/claude-code)
- [MCP 协议规范](https://modelcontextprotocol.io)
- [Skills 开发指南](https://docs.anthropic.com/claude-code/skills)
- [社区分享](https://github.com/anthropics/claude-code-examples)

---

*最后更新: 2026-01-30*
*作者: toboto*
