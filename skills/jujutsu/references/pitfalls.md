# 常见错误与陷阱

> 基于官方文档，Agent 容易犯的错误。

## 🔴 严重错误

### 用 `git add`

**错误**：想暂存文件时用 `git add`

**问题**：jj 没有暂存区概念，`git add` 不会生效

**正确做法**：
```bash
# jj 自动追踪所有修改，直接提交即可
jj commit -m "message"

# 如果只想提交部分文件，用 jj split
jj split file1 file2
```

### 用 `jj co` 或 `jj checkout` 切换

**错误**：用 `jj co <bookmark>` 或 `jj checkout`

**问题**：jj 根本没有这两个命令！

**正确做法**：
```bash
# 创建新 change 在 bookmark 上（相当于 checkout -b）
jj new main

# 创建新 change 并设置 bookmark
jj new main -b myfeature

# 编辑现有 commit
jj edit <revision>
```

### 用 `git stash` 暂存

**错误**：用 `git stash`

**问题**：jj 没有 stash，用 `jj new @-` 创建兄弟 commit

**正确做法**：
```bash
# 临时保存当前工作（创建兄弟 commit）
jj new @-

# 恢复：用 jj edit 回到原 commit
jj edit <原commit>
```

### 用 `git merge`

**错误**：用 `jj merge`

**问题**：jj 没有 merge 命令

**正确做法**：
```bash
# 合并 A 到当前 commit
jj new @ A
```

## 🟠 易错操作

### 混淆 `-b` 和 `-s` 在 rebase

**误解**：`-b` 移动单个 commit

**正确**：
- `-b <bookmark>`：移动 bookmark 指向的 commit（不包含后代）
- `-s <commit>`：移动 commit 及其所有后代

```bash
# 错误
jj rebase -b A -o B  # 移动 A（不含后代）

# 正确（移动 A 及其后代）
jj rebase -s A -o B
```

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

### 冲突后不知如何继续

**误解**：遇到冲突必须立即解决

**正确**：jj 允许先继续工作，稍后再解决

```bash
# 冲突后，jj 会创建 conflicted change
# 可以继续创建新 commit
jj new

# 之后回到冲突 commit 解决
jj new <conflicted-commit>
# 解决文件中的冲突
jj resolve <file>
jj squash
```

### 用 `jj file untrack` 但不设置 ignore

**错误**：直接 `jj file untrack`

**问题**：文件必须匹配 ignore pattern 才能 untrack

**正确做法**：
```bash
# 1. 先添加到 .gitignore
echo "file.txt" >> .gitignore

# 2. 再 untrack
jj file untrack file.txt
```

### 混淆 bookmarks 和 changes

**误解**：bookmark 就是 branch

**正确**：
- **Bookmark**：类似 Git branch，是指向提交的指针
- **Change**：jj 核心概念，是可编辑的提交
- **Working-copy commit**：当前工作目录的 commit（@ 符号）
- **无"当前 bookmark"** — jj 没有活跃分支的概念

### 忽略 divergent changes

**误解**：只要用 change ID 就不会有歧义

**正确**：如果 change ID 分叉了，需要用 commit ID 或带偏移的 change ID

```bash
# 分叉的 change ID
jj log  # 显示为 xyz/0, xyz/1

# 用 commit ID 指定
jj edit <commit-id>

# 或用带偏移的 change ID
jj edit xyz/0
```

## 🟡 小问题

### 忘记 `-m` 参数

**问题**：`jj commit` 不带 `-m` 会打开编辑器

**建议**：习惯用 `jj commit -m "message"`

### 在 Git 项目中直接用 `git init`

**问题**：应该用 `jj git init`

**正确**：
```bash
jj git init
# 或
jj git clone <url>
```

### 混淆 tracked vs untracked bookmarks

**误解**：fetch 后自动跟踪

**正确**：
```bash
# 默认只跟踪 origin 的 main
# 其他需要手动 track
jj bookmark track <name> --remote=<remote>

# 查看tracked
jj bookmark list --tracked
```

## 检查清单

操作前快速检查：
- [ ] 不要用 `git add`
- [ ] 不要用 `jj co` 或 `jj checkout`
- [ ] 用 `jj commit` 而不是 `git commit`
- [ ] 用 `jj bookmark` 而不是 `git branch`
- [ ] 用 `jj new @ A` 而不是 `git merge`
- [ ] 用 `jj rebase -b` 或 `-s` 变基
- [ ] 用 `jj new @-` 暂存而不是 `git stash`
- [ ] 分叉的 change ID 需要用 commit ID 明确指定
