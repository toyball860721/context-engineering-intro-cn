# Context Engineering 中文精简版

> 📘 让 AI 真正理解你的项目 — Context Engineering 实战指南
> 
> 📦 基于 [coleam00/context-engineering-intro](https://github.com/coleam00/context-engineering-intro) (12,963⭐)
> 
> 🚀 10 分钟上手，让 Claude Code 产出高质量代码

---

## ⚡ 什么是 Context Engineering？

**简单说：给 AI 足够的上下文，让它像你的团队成员一样思考。**

### 对比

| 方法 | 效果 | 比喻 |
|------|------|------|
| Prompt Engineering | 60 分 | 给陌生人发便利贴 |
| **Context Engineering** | **95 分** | **给团队成员完整项目文档** |
| Vibe Coding | 30 分 | 靠感觉瞎猜 |

---

## 🎯 核心工作流

```
1. 写 INITIAL.md（描述你想做什么）
   ↓
2. 运行 /generate-prp INITIAL.md
   ↓
3. AI 生成完整的 PRP（实现蓝图）
   ↓
4. 运行 /execute-prp PRPs/xxx.md
   ↓
5. AI 按蓝图实现功能 + 自动验证
```

---

## 📁 项目结构

```
context-engineering-intro-cn/
├── .claude/commands/
│   ├── generate-prp.md    # 生成 PRP 的命令
│   └── execute-prp.md     # 执行 PRP 的命令
├── PRPs/                   # 存放生成的 PRP
├── examples/               # 你的代码示例（关键！）
├── CLAUDE.md              # 项目全局规则
├── INITIAL.md             # 功能请求模板
└── README.md              # 本文件
```

---

## 🛠️ 快速使用

### Step 1: 克隆项目

```bash
git clone https://github.com/toyball860721/context-engineering-intro-cn.git
cd context-engineering-intro-cn
```

### Step 2: 配置 Claude Code

在 Claude Code 中运行：

```bash
# 添加本项目到 Claude Code 的上下文
claude mcp add context-engineering npx @your/config
```

### Step 3: 写功能请求

编辑 `INITIAL.md`：

```markdown
## FEATURE:
构建一个用户登录系统，支持邮箱 + 密码、Google OAuth、JWT 认证

## EXAMPLES:
- examples/auth/jwt-example.js - JWT 生成和验证模式
- examples/database/user-model.js - 用户数据模型

## DOCUMENTATION:
- https://jwt.io/introduction
- https://developers.google.com/identity/protocols/oauth2

## OTHER CONSIDERATIONS:
- 密码必须 bcrypt 加密（cost=12）
- JWT 过期时间 7 天
- 需要速率限制（每 IP 每分钟 5 次登录）
```

### Step 4: 生成 PRP

在 Claude Code 中运行：

```bash
/generate-prp INITIAL.md
```

等待 1-2 分钟，AI 会生成一个完整的 PRP 文件（通常 2000-5000 字）。

### Step 5: 执行 PRP

```bash
/execute-prp PRPs/user-login-system.md
```

AI 开始实现，自动运行测试，修复错误，直到完成。

---

## 📝 INITIAL.md 写作模板

### 好的示例

```markdown
## FEATURE:
构建异步网络爬虫，使用 Playwright，支持：
- 并发抓取（最多 10 个页面同时）
- 自动重试（失败 3 次后放弃）
- 数据导出（CSV + JSON）
- 速率限制（每域名每秒 1 请求）

## EXAMPLES:
- examples/playwright/basic-crawler.js - 基础爬虫模式
- examples/database/result-storage.js - 数据存储模式

## DOCUMENTATION:
- https://playwright.dev/docs/api/class-browser
- https://nodejs.org/api/stream.html

## OTHER CONSIDERATIONS:
- 需要处理反爬虫（随机 User-Agent）
- 内存限制：同时最多 100 个页面
- 需要日志记录（winston，级别：info）
```

### 坏的示例

```markdown
## FEATURE:
做个爬虫

## EXAMPLES:
无

## DOCUMENTATION:
无

## OTHER CONSIDERATIONS:
无
```

---

## 💡 高级技巧

### 1. 建立示例库

```
examples/
├── api/
│   ├── rest-call.js
│   ├── graphql-query.js
│   └── rate-limiting.js
├── database/
│   ├── postgres-connection.js
│   ├── transaction-example.js
│   └── migration-pattern.js
└── testing/
    ├── unit-test-template.js
    └── integration-test-setup.js
```

### 2. 定制 CLAUDE.md

```markdown
# 项目规则

## 代码风格
- 使用 TypeScript
- 函数不超过 50 行
- 必须写 JSDoc 注释

## 测试要求
- 新功能必须有单元测试
- 覆盖率 > 80%
- 使用 Jest

## 禁止事项
- 不要使用 any 类型
- 不要写超过 3 层的嵌套
- 不要忽略错误处理
```

### 3. 多 PRP 协作

复杂项目拆成多个 PRP：

```bash
/generate-prp INITIAL_backend.md
/generate-prp INITIAL_frontend.md
/generate-prp INITIAL_deployment.md
```

---

## 🎓 实战案例

### 案例 1：API 集成

```markdown
## FEATURE:
集成 Stripe 支付，支持：
- 一次性付款
- 订阅付款
- Webhook 处理

## EXAMPLES:
- examples/stripe/checkout-session.js
- examples/webhook/handler-template.js

## OTHER CONSIDERATIONS:
- 测试模式用 Stripe Test Keys
- Webhook 必须验证签名
- 错误要记录到 Sentry
```

### 案例 2：数据库迁移

```markdown
## FEATURE:
添加用户表，包含：
- 基础信息（email, password_hash, created_at）
- 个人资料（name, avatar_url, bio）
- 索引（email 唯一索引）

## EXAMPLES:
- examples/migrations/20240101_create_posts.js

## OTHER CONSIDERATIONS:
- 使用 Knex migration
- 必须可回滚
- 添加 seed 数据
```

---

## ❓ 常见问题

### Q: 适合什么规模的项目？

A: 任何规模。小项目（100 行）到大项目（10 万 + 行）都适用。

### Q: 每个功能都要写 INITIAL.md 吗？

A: 是的。这确保 AI 有清晰、独立的上下文。

### Q: AI 不遵循示例怎么办？

A: 在 CLAUDE.md 中更明确："始终遵循 examples/ 中的模式"。

### Q: 可以用于其他 AI 吗？

A: 可以！原则适用于 Cursor、Codex、Gemini CLI 等。

---

## 📚 深入学习

- [完整中文文档](./README.md)
- [英文原版项目](https://github.com/coleam00/context-engineering-intro)
- [Claude Code 官方文档](https://docs.anthropic.com/claude-code)

---

## 🤝 反馈与交流

- [提交 Issue](https://github.com/toyball860721/context-engineering-intro-cn/issues)
- [加入讨论](https://github.com/toyball860721/context-engineering-intro-cn/discussions)

---

## ☕ 支持本项目

- [爱发电](https://afdian.com/a/toyball)
- [GitHub Sponsors](https://github.com/sponsors/toyball860721)

---

**🦞 中文维护者：[@toyball860721](https://github.com/toyball860721)**

*最后更新：2026-03-28*
