---
name: git-commit-style
description: "规范化生成中文 git commit 信息。Use when 任何git提交的场景"
---

# Git Commit Style

## 核心格式

使用 Conventional Commits 风格，并用中文描述变更：

```text
type(scope): 中文提交说明
```

示例：

```text
feat(player): 增加播放队列循环模式
fix(floating-ball): 修复拖拽后位置丢失
docs(ai2ai): 更新悬浮球 API 文档
test(storage): 补充歌单导入测试
refactor(core): 简化播放上下文选择逻辑
```

## Scope 选择

scope 使用小写英文、数字或连字符，保持短而稳定。优先用模块、目录、功能边界或文档域

无法确定明确模块时，可以省略 scope：

```text
chore: 整理项目维护配置
```

## 提交拆分

开发过程中，生产代码、SPEC 文档和测试代码必须分别提交，不得混在同一个 commit 中：

- 生产代码使用 `feat`、`fix`、`refactor` 等与变更性质匹配的类型。
- SPEC 文档使用 `docs`，scope 优先标明 `me2ai`、`ai2ai` 或对应文档域。
- 测试代码使用 `test`，scope 优先标明被验证的模块。

同一工作区同时包含以上多类改动时，按文件或变更块分别暂存并创建多个 commit。生成提交方案或执行提交前，先检查暂存区，确保每个 commit 只包含一种类别的变更。这一拆分用于支持按提交选择性发布，例如只将生产代码 cherry-pick 到不包含 SPEC 和测试的分支。

## 生成前检查

生成 commit message 前先判断：

- 主要变化是什么。
- 生产代码、SPEC 文档和测试代码是否已分别提交。
- 同一类别内是否仍存在需要独立审阅或独立发布的变更，应继续拆分。
- 是否涉及 API、协议、持久化或文档同步。
- 是否已经运行用户或项目要求的验证命令。
- scope 是否稳定且能帮助未来检索。

如果用户提供了 `git diff`、`git status` 或变更摘要，基于实际变化生成提交信息；不要凭空加入未发生的改动。
