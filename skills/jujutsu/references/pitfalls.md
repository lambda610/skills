# 常见错误与陷阱

> Agent 容易犯的错误，按严重程度排序。

## 🔴 严重错误

### 用 `git add`

**错误**：想暂存文件时用 `git add`

**问题**：jj 没有暂存区概念，`git add` 不会生效（除非在 git 兼容模式）

**正确做法**：
```bash
# jj 自动追踪所有修改，直接提交即可
jj commit -m "message"

# 如果只想提交部分文件，用 jj split 或 jj diffedit
jj diffedit -r @
```

### 用 `git checkout` 切换分支

**错误**：用 `git checkout <bookmark>` 切换分支

**问题**：jj 用 `jj co` 或 `jj edit`

**正确做法**：
```bash
jj co <bookmark>
# 或
jj edit <bookmark>
```

### 用 `git stash` 暂存

**错误**：用 `git stash` 暂存改动

**问题**：jj 用 shelf

**正确做法**：
```bash
# 暂存当前改动
jj shelf

# 恢复暂存
jj shelf unapply

# 查看暂存列表
jj shelf list
```

## 🟠 易错操作

### `jj new` 不带参数

**误解**：`jj new` 等于 `git checkout -b`

**正确**：`jj new` 基于当前 `@` 创建新 change，不带 bookmark 名

```bash
# 创建新 change（无 bookmark）
jj new

# 创建并设置 bookmark
jj new -b <bookmark>

# 基于某提交创建
jj new <revision>
```

### `jj rebase` 参数顺序

**误解**：先写源后写目标（像 git 那样）

**正确**：jj 用 `-b` 指定要移动的 bookmark，`-o` 指定目标位置

```bash
# 错误
jj rebase A B  # ❌

# 正确
jj rebase -b A -o B  # ✅ 把 A 变基到 B 上
```

### 冲突后继续操作

**误解**：遇到冲突必须解决才能继续

**正确**：jj 允许先继续工作，稍后再解决冲突

```bash
# 冲突后，先查看状态
jj st

# 创建新 change 继续工作（冲突会保留在原 change）
jj new

# 之后回到冲突的 change，解决后再 squash
jj co <conflict-change>
# 解决冲突文件
jj resolve <file>
jj squash
```

## 🟡 小问题

### 忘记 `-m` 参数

**问题**：`jj commit` 不带 `-m` 会打开编辑器

**建议**：习惯用 `jj commit -m "message"`

### 混淆 bookmarks 和 changes

- **Bookmark**：类似 Git branch，是指向提交的指针
- **Change**：jj 的核心概念，是可编辑的提交

```
@ → 当前工作的 change
HEAD → 当前 checkout 的 bookmark 指向的提交
```

### 用 Git 命令

**提醒**：在 jj 项目中尽量用 jj 命令。虽然 jj 兼容 git 操作，但：
- `jj git init` 初始化 `.jj/` 目录
- `jj git clone` 正确设置 jj 环境
- 直接用 `git init` 可能导致 jj 无法识别

## 检查清单

操作前快速检查：
- [ ] 不要用 `git add`
- [ ] 用 `jj commit` 而不是 `git commit`
- [ ] 用 `jj co` 而不是 `git checkout`
- [ ] 用 `jj bookmark` 而不是 `git branch`
- [ ] 用 `jj rebase -b -o` 而不是 `git rebase`
- [ ] 用 `jj shelf` 而不是 `git stash`
