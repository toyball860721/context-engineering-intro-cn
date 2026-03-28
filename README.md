# Context Engineering 入门指南（中文版）

> 📘 **Context Engineering（上下文工程）** — 让 AI 编码助手真正理解你的项目
> 
> 🔥 **Context Engineering 比 Prompt Engineering 强 10 倍，比 Vibe Coding 强 100 倍**
> 
> 📦 原版项目：[coleam00/context-engineering-intro](https://github.com/coleam00/context-engineering-intro) (12,963⭐)
> 
> 📝 中文维护者：[@toyball860721](https://github.com/toyball860721)
> 
> ☕ 支持本项目：[爱发电](https://afdian.com/a/toyball) | [GitHub Sponsors](https://github.com/sponsors/toyball860721)

---

## 🚀 快速开始

```bash
# 1. 克隆本模板
git clone https://github.com/toyball860721/context-engineering-intro-cn.git
cd context-engineering-intro-cn

# 2. 设置项目规则（可选 - 已提供模板）
# 编辑 CLAUDE.md 添加你的项目特定指南

# 3. 添加示例（强烈推荐）
# 将相关代码示例放入 examples/ 文件夹

# 4. 创建初始功能请求
# 编辑 INITIAL.md 填写你的功能需求

# 5. 生成完整的 PRP（产品需求提示）
# 在 Claude Code 中运行：
/generate-prp INITIAL.md

# 6. 执行 PRP 实现你的功能
# 在 Claude Code 中运行：
/execute-prp PRPs/your-feature-name.md
```

---

## 📚 目录

- [什么是 Context Engineering？](#什么是-context-engineering)
- [模板结构](#模板结构)
- [分步指南](#分步指南)
- [编写有效的 INITIAL.md](#编写有效的-initialmd)
- [PRP 工作流](#prp-工作流)
- [有效使用示例](#有效使用示例)
- [最佳实践](#最佳实践)

---

## 什么是 Context Engineering？

Context Engineering 代表了与传统 Prompt Engineering 的范式转变：

### Prompt Engineering vs Context Engineering

**Prompt Engineering（提示工程）：**
- 专注于巧妙的措辞和特定措辞
- 局限于如何描述任务
- 就像给别人一张便利贴

**Context Engineering（上下文工程）：**
- 一个提供全面上下文的完整系统
- 包括文档、示例、规则、模式和验证
- 就像写一部完整的剧本，包含所有细节

### 为什么 Context Engineering 很重要

1. **减少 AI 失败**：大多数 agent 失败不是模型失败，而是上下文失败
2. **确保一致性**：AI 遵循你的项目模式和约定
3. **实现复杂功能**：AI 可以处理多步骤实现
4. **自我纠正**：验证循环允许 AI 修复自己的错误

---

## 模板结构

```
context-engineering-intro-cn/
├── .claude/
│   ├── commands/
│   │   ├── generate-prp.md    # 生成完整的 PRP
│   │   └── execute-prp.md     # 执行 PRP 实现功能
│   └── settings.local.json    # Claude Code 权限配置
├── PRPs/
│   ├── templates/
│   │   └── prp_base.md       # PRP 基础模板
│   └── EXAMPLE_multi_agent_prp.md  # 完整 PRP 示例
├── examples/                  # 你的代码示例（关键！）
├── CLAUDE.md                 # AI 助手的全局规则
├── INITIAL.md               # 功能请求模板
├── INITIAL_EXAMPLE.md       # 功能请求示例
└── README.md                # 本文件
```

---

## 分步指南

### 1. 设置全局规则（CLAUDE.md）

`CLAUDE.md` 文件包含 AI 助手在每次对话中遵循的项目级规则。模板包括：

- **项目意识**：阅读规划文档、检查任务
- **代码结构**：文件大小限制、模块组织
- **测试要求**：单元测试模式、覆盖率期望
- **风格约定**：语言偏好、格式化规则
- **文档标准**：文档字符串格式、注释实践

**你可以直接使用提供的模板，或根据你的项目定制。**

### 2. 创建初始功能请求

编辑 `INITIAL.md` 描述你想构建的内容：

```markdown
## FEATURE:
[描述你想构建的功能 - 具体说明功能和需求]

## EXAMPLES:
[列出 examples/ 文件夹中的示例文件并解释如何使用]

## DOCUMENTATION:
[包含相关文档、API 或 MCP 服务器资源的链接]

## OTHER CONSIDERATIONS:
[提及任何陷阱、特定需求或 AI 助手容易忽略的事项]
```

**参见 `INITIAL_EXAMPLE.md` 获取完整示例。**

### 3. 生成 PRP

PRP（Product Requirements Prompts，产品需求提示）是全面的实现蓝图，包括：

- 完整的上下文和文档
- 带验证的实现步骤
- 错误处理模式
- 测试要求

它们类似于 PRD（产品需求文档），但专门为指导 AI 编码助手而设计。

在 Claude Code 中运行：
```bash
/generate-prp INITIAL.md
```

**注意：** 斜杠命令是在 `.claude/commands/` 中定义的自定义命令。你可以查看它们的实现：
- `.claude/commands/generate-prp.md` - 查看如何研究和创建 PRP
- `.claude/commands/execute-prp.md` - 查看如何从 PRP 实现功能

`$ARGUMENTS` 变量接收你在命令名后传递的任何内容（例如 `INITIAL.md` 或 `PRPs/your-feature.md`）。

此命令将：
1. 读取你的功能请求
2. 研究代码库以查找模式
3. 搜索相关文档
4. 在 `PRPs/your-feature-name.md` 中创建完整的 PRP

### 4. 执行 PRP

生成后，执行 PRP 来实现你的功能：

```bash
/execute-prp PRPs/your-feature-name.md
```

AI 编码助手将：
1. 读取 PRP 中的所有上下文
2. 创建详细的实现计划
3. 执行每个步骤并进行验证
4. 运行测试并修复任何问题
5. 确保满足所有成功标准

---

## 编写有效的 INITIAL.md

### 关键部分说明

**FEATURE：要具体和全面**
- ❌ "构建一个网络爬虫"
- ✅ "使用 BeautifulSoup 构建异步网络爬虫，从电商网站提取产品数据，处理速率限制，并将结果存储在 PostgreSQL 中"

**EXAMPLES：利用 examples/ 文件夹**
- 将相关代码模式放入 `examples/`
- 引用特定文件和要遵循的模式
- 解释应该模仿哪些方面

**DOCUMENTATION：包含所有相关资源**
- API 文档 URL
- 库指南
- MCP 服务器文档
- 数据库模式

**OTHER CONSIDERATIONS：捕获重要细节**
- 认证要求
- 速率限制或配额
- 常见陷阱
- 性能要求

---

## PRP 工作流

### /generate-prp 如何工作

该命令遵循以下流程：

1. **研究阶段**
   - 分析你的代码库以查找模式
   - 搜索类似实现
   - 识别要遵循的约定

2. **文档收集**
   - 搜索相关 API 文档
   - 查找库使用示例
   - 收集技术参考

3. **PRP 创建**
   - 编写全面的实现计划
   - 包含验证步骤
   - 定义成功标准

### /execute-prp 如何工作

执行命令时，AI 助手：

1. **理解上下文**
   - 阅读所有提供的文档
   - 理解项目模式
   - 识别约束条件

2. **制定计划**
   - 分解为可管理的步骤
   - 确定依赖关系
   - 规划验证点

3. **执行与验证**
   - 逐步实现
   - 每个步骤后运行测试
   - 根据需要迭代修复

---

## 有效使用示例

### 示例的力量

示例是 Context Engineering 中最强大的工具之一：

- **展示而非讲述**：AI 从具体代码中学习最好
- **确保一致性**：AI 模仿现有模式
- **减少错误**：AI 遵循经过验证的模式

### 放置示例的位置

```
examples/
├── api-calls/           # API 调用示例
├── database/            # 数据库操作示例
├── error-handling/      # 错误处理示例
├── testing/             # 测试模式示例
└── ui-components/       # UI 组件示例
```

### 编写好示例的技巧

1. **保持简洁**：只展示相关模式
2. **添加注释**：解释关键决策
3. **包含测试**：展示如何验证
4. **文档化陷阱**：警告常见问题

---

## 最佳实践

### ✅ 应该做的

- **从 INITIAL.md 开始**：始终先写下你的想法
- **使用示例**：提供代码示例供 AI 模仿
- **迭代改进**：根据结果改进你的上下文
- **记录决策**：在 CLAUDE.md 中记录项目决策
- **运行验证**：始终验证 AI 的输出

### ❌ 不应该做的

- **不要假设上下文**：明确说明一切
- **不要跳过示例**：示例至关重要
- **不要一次性全部完成**：迭代构建
- **不要忘记更新**：随着项目发展更新上下文

---

## 进阶技巧

### 1. 创建领域特定模板

为你的特定用例创建专门的模板：

```
templates/
├── api-integration/     # API 集成模板
├── database-migration/  # 数据库迁移模板
├── ui-component/        # UI 组件模板
└── test-suite/          # 测试套件模板
```

### 2. 使用多个 PRP

对于复杂功能，创建多个相互关联的 PRP：

```bash
/generate-prp INITIAL_part1.md
/generate-prp INITIAL_part2.md
```

### 3. 建立验证循环

在 PRP 中包含自动验证：

```markdown
## Validation Steps
1. Run `npm test` - all tests must pass
2. Run `npm run lint` - no errors
3. Manual testing: [specific steps]
4. Performance check: [metrics]
```

---

## 常见问题

### Q: Context Engineering 适合什么规模的项目？

A: 从小型项目（100 行代码）到大型项目（10 万 + 行代码）都适用。关键是上下文的组织方式。

### Q: 我需要为每个功能创建 INITIAL.md 吗？

A: 是的，每个功能都应该有自己的 INITIAL.md。这确保 AI 有清晰的上下文。

### Q: 如果 AI 没有遵循我的示例怎么办？

A: 在 CLAUDE.md 中更明确地说明。例如："始终遵循 examples/ 中的错误处理模式"。

### Q: 可以将此用于其他 AI 助手吗？

A: 可以！虽然这是为 Claude Code 设计的，但原则适用于任何 AI 编码助手。

---

## 学习资源

- [英文原版项目](https://github.com/coleam00/context-engineering-intro)
- [Claude Code 文档](https://docs.anthropic.com/claude-code)
- [MCP 协议规范](https://modelcontextprotocol.io)

---

## 🤝 参与贡献

欢迎提交 Issue 和 Pull Request 改进中文文档！

- 报告翻译错误
- 补充使用示例
- 添加更多中文教程

---

## 📄 许可证

本项目遵循原项目的 MIT 许可证。

---

## ☕ 支持作者

如果你觉得这个中文文档对你有帮助，欢迎支持：

- [爱发电](https://afdian.com/a/toyball)
- [GitHub Sponsors](https://github.com/sponsors/toyball860721)

**中文维护者持续更新中...** 🦞

*最后更新：2026-03-28*
