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
| `git add` | jj 无暂存区，不需要 add |
| commit 后不能改 | jj 的 commit 是可编辑的 change |
| 用 branch 管理分支 | jj 用 bookmarks，是轻量指针 |
| `git stash` 暂存 | 用 `jj new @-` |
| 冲突必须立即解决 | jj 冲突可延迟处理 |
| checkout 切换 | 用 `jj edit`（无 checkout） |

### ✅ 正确的心智模型

1. **自动追踪** — jj 自动追踪所有修改，无需 `git add`
2. **可变提交** — commit 是可编辑的"change"，随时可修改
3. **操作可撤销** — 几乎所有操作都能用 `jj undo` 撤销
4. **Bookmarks** — 轻量标记，类似 Git branch 但有 tracked 概念
5. **Revsets** — 强大的查询语法，能表达复杂条件
6. **无 checkout** — 用 `jj edit` 切换到某 commit
7. **冲突不阻塞** — 冲突记录在 commit 中，可稍后解决

## 核心概念

### Change vs Commit

- **Commit**：文件的快照 + 元数据（作者、日期、父提交）
- **Change**：commit 的演化历史，用 change ID 标识（类似 Gerrit 的 Change-Id）
- **Working-copy commit**：当前工作目录对应的 commit（@ 符号）

### Change ID vs Commit ID

- **Change ID**：jj 特有，16 字节随机生成，格式如 `kntqzsqt`，会保持不变
- **Commit ID**：Git 兼容的提交哈希，会随内容变化

### Bookmark vs Branch

- **Bookmark**：指向 commit 的命名指针，类似 Git branch
- **无"当前 bookmark"** — jj 没有活跃分支的概念
- **Tracked bookmark**：自动跟踪远程同名 bookmark

### Colocated Workspaces

jj 和 git 可共存于同一目录：
- `.jj/` + `.git/` 共存
- jj 和 git 命令可混用
- jj 自动 import/export 到 git

## 常用命令速查

```bash
# 查看状态
jj st                    # 当前变更（相当于 git status）
jj log                   # 历史
jj log --graph           # 图形化历史

# 操作变更（无需 add）
jj diff                  # 查看当前变更
jj describe             # 修改提交信息
jj commit -m "message"  # 提交（自动包含所有修改）
jj squash               # 合并到父提交（类似 git commit --amend）
jj restore <path>       # 撤销文件修改

# ⚠️ 没有 checkout！
# 切换到某 commit 编辑：用 jj edit <revision>
# 创建新 change：用 jj new

# 创建与切换
jj new                  # 创建新 empty change（当前 @ 的子提交）
jj new <revision>       # 基于某 revision 创建新 change
jj new -b <bookmark>   # 创建新 change 并设置 bookmark
jj edit <revision>      # 切换到某 commit 进行编辑（类似 checkout）

# Bookmarks
jj bookmark list         # 列出 bookmarks
jj bookmark create <name> -r <revision>  # 创建 bookmark
jj bookmark delete <name>  # 删除 bookmark
jj bookmark move <name> --to <revision>  # 移动 bookmark
jj bookmark track <name> --remote=<remote>  # 跟踪远程 bookmark

# 变基
jj rebase -b <bookmark> -o <dest>  # 移动整个分支
jj rebase -s <commit> -o <dest>    # 移动 commit 及其后代
jj rebase -r <commit> -o <dest>    # 只移动指定 commit

# 远程操作
jj git fetch             # 拉取
jj git push              # 推送
jj git push --bookmark <name>  # 推送特定 bookmark

# 撤销
jj undo                  # 撤销上一次操作
jj op log                # 查看操作日志

# 多远程
jj config set --user git.fetch '["upstream", "origin"]'
jj bookmark track main --remote=origin  # 跟踪 origin/main
```

## 常见工作流

### 日常提交
```bash
# 1. 查看变更
jj st
jj diff

# 2. 提交（无需 add！）
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

# 把变更 squash 到指定提交
jj squash --into <commit>
```

### 编辑现有 commit（类似 git checkout）
```bash
# 切换到某 commit 进行编辑
jj edit <revision>

# 之后的所有修改都会 amend 这个 commit
```

### 创建新分支
```bash
# 创建新 change 并设置 bookmark
jj new main -b topic
```

### 变基
```bash
# 移动整个分支（包含所有后代）
jj rebase -b topic -o main

# 移动单个 commit 及其后代
jj rebase -s <commit> -o <dest>

# 只移动单个 commit（不包含后代）
jj rebase -r <commit> -o <dest>
```

### 处理冲突
```bash
# 1. 冲突不会中断操作，会创建 conflicted change
# 2. 创建新 commit 来解决冲突
jj new <conflicted-commit>

# 3. 解决文件中的冲突标记
# 编辑文件...

# 4. 标记已解决
jj resolve <file>

# 5. squash 到原提交
jj squash
```

### 临时保存当前工作
```bash
# 相当于 git stash：创建兄弟 commit
jj new @-

# 恢复：用 jj edit <commit> 回到之前的 commit
```

### Divergent Changes（分叉变化）

当同一 change ID 有多个可见 commit 时：
```bash
# 查看
jj log  # 显示 divergent 标记

# 解决策略
jj abandon <unwanted-commit-id>  # 放弃一个
jj metaedit --update-change-id <commit-id>  # 生成新 change ID
jj squash --from <source> --into <target>  # 合并两个
```

## 关键命令对照

| Git | Jujutsu | 说明 |
|-----|---------|------|
| `git status` | `jj st` | |
| `git diff` | `jj diff` | |
| `git add` | ❌ 不需要 | jj 自动追踪 |
| `git commit` | `jj commit -m "msg"` | |
| `git commit --amend` | `jj squash` | |
| `git checkout <commit>` | `jj edit <revision>` | **切换到某 commit 编辑** |
| `git checkout -b <name>` | `jj new <base> -b <name>` | 创建并设置 bookmark |
| `git branch` | `jj bookmark list` | |
| `git switch <branch>` | `jj new <bookmark>` | **创建新 change** |
| `git merge A` | `jj new @ A` | 创建 merge commit |
| `git rebase A B` | `jj rebase -s A -o B` | A 及其后代移到 B 上 |
| `git stash` | `jj new @-` | |
| `git reset --hard` | `jj abandon` | |
| `git reflog` | `jj op log` | |

**注意**：
- `jj new` **不是** `git checkout`，而是创建新 change
- `jj edit` 才是类似"切换到某 commit"的命令

## 注意事项

1. **不要用 `git add`** — jj 自动追踪
2. **没有 checkout** — 用 `jj edit` 切换，用 `jj new` 创建
3. **`jj commit` 自动包含所有修改** — 不需要 `-a`
4. **冲突不阻塞** — 可以继续工作，稍后再解决
5. **`jj new` 创建的是 change** — 是可编辑的空 commit
6. **Bookmarks 有 tracked 概念** — 类似 Git 的 upstream

## Revset 快速参考

```bash
# 常用符号
@       # 当前 working-copy commit
@-      # 父提交
root()  # 根提交
bookmarks()  # 所有 bookmark

# 运算符
::      # 祖先（包含自己）
..      # 不包含祖先
~       # 差集
|       # 并集
&       # 交集

# 示例
jj log -r ::@           # 当前 commit 的祖先链
jj log -r 'all()'       # 所有可见 commit
jj log -r main..        # main 分支后的 commit
```

## 获取帮助

```bash
jj help
jj help <subcommand>
```

更多内容：见 `references/` 目录
