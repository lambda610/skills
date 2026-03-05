---
name: jujutsu
description: Use Jujutsu (jj) for version control in jj-enabled projects. Applies when the project uses jj (has .jj/ directory, README specifies jj, or user requests jj).
---

# Jujutsu 使用指南

Jujutsu (jj) 是新一代分布式版本控制工具，兼容 Git 仓库但用法有根本差异。

## 何时使用

**仅在明确使用 jj 的项目中使用此 skill。** 判断方法：
- 存在 `.jj/` 目录
- 项目 README 明确要求用 jj
- 用户明确指定用 jj

对于普通 Git 项目，使用标准的 Git 工具。

## 心智模型（与 Git 的根本差异）

### ❌ 不要按 Git 思维操作

| Git 思维 | 问题 |
|---------|------|
| `git add` → `git commit` | jj 无暂存区，不需要 add |
| commit 后不能改 | jj 的 commit 可随时修改 |
| 用 branch 管理分支 | jj 用 bookmarks，是轻量指针 |
| stash 暂存改动 | jj 用 shelf 或直接新建 change |
| 冲突必须立即解决 | jj 先继续工作，之后再解决 |

### ✅ 正确的心智模型

1. **自动追踪** — jj 自动追踪所有修改，无需 `git add`
2. **可变提交** — commit 是可编辑的"change"，随时可修改
3. **操作可撤销** — 几乎所有操作都能用 `jj undo` 撤销
4. **Bookmarks** — 轻量标记，不是 Git branch 的完全等价物
5. **Revsets** — 强大的查询语法，能表达复杂条件

## 常用命令速查

```bash
# 查看状态
jj st                    # 当前变更
jj log                   # 历史（按时间倒序）
jj log --graph           # 图形化历史

# 操作变更
jj diff                  # 查看当前变更
jj describe              # 修改提交信息
jj commit -m "message"   # 提交（会自动包含所有修改）
jj squash                # 合并到父提交
jj restore <path>        # 撤销文件修改

# Bookmarks（类似 branch）
jj bookmark list         # 列出 bookmarks
jj bookmark create <name>  # 创建 bookmark
jj bookmark delete <name>  # 删除 bookmark
jj bookmark move <name> --to <rev>  # 移动 bookmark

# 分支/工作流
jj new                   # 创建新 change
jj new <rev>             # 基于某提交创建新 change
jj co <bookmark>         # 切换到 bookmark
jj rebase -b <bookmark> -o <dest>  # 变基

# 远程操作
jj git fetch             # 拉取
jj git push              # 推送
jj git push --bookmark <name>  # 推送特定 bookmark

# 撤销
jj undo                  # 撤销上一次操作
jj op log                # 查看操作日志
```

## 常见工作流

### 日常提交
```bash
# 1. 查看变更
jj st
jj diff

# 2. 提交（无需 add）
jj commit -m "feat: add new feature"

# 3. 查看历史
jj log
```

### 修改历史提交
```bash
# 修改当前提交的描述
jj describe -m "new message"

# 把当前变更合并到上一个提交
jj squash

# 拆分当前提交（需要用 jj diffedit）
jj split
```

### 处理冲突
```bash
# 1. 冲突时 jj 不会中断，会创建一个 conflicted change
# 2. 解决文件冲突后
jj resolve <file>

# 3. 确认解决完毕
jj st

# 4. 继续提交或 squash
jj squash
```

### 与远程同步
```bash
# 拉取远程变更
jj git fetch

# 如果有冲突，创建新 change 再处理
jj new <remote>/main

# 推送
jj git push
```

## 注意事项

1. **不要用 `git add`** — jj 自动追踪，add 反而可能造成混淆
2. **不要用 `git checkout <file>`** — 用 `jj restore <file>`
3. **不要用 `git stash`** — 用 `jj shelf` 或新建 change
4. **`jj commit` 会包含所有修改** — 不需要 `-a` 之类 flag
5. **冲突不阻塞** — 可以继续工作，稍后再解决

## 获取帮助

```bash
jj help
jj help <subcommand>
jj log --help  # 查看 revset 语法
```

更多命令对照：见 `references/commands.md`
