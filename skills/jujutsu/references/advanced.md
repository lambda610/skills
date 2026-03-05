# 高级主题

> 基于官方文档的补充内容

## Colocated Workspaces（共存工作区）

jj 和 git 可以共存于同一目录，方便迁移和混用工具。

### 创建

```bash
# 新建共存工作区（默认行为）
jj git init
# 或
jj git clone <url>

# 禁用共存
jj git init --no-colocate
jj git clone --no-colocate <url>
```

### 混用 jj 和 git

```bash
# 在共存工作区中可以：
jj st
git status  # 也可以用，但可能显示"detached HEAD"

# jj 命令会自动 import/export 到 git
# 但建议主要用 jj，git 只做只读操作
```

### 切换共存状态

```bash
# 查看当前状态
jj git colocation status

# 启用共存
jj git colocation enable

# 禁用共存
jj git colocation disable
```

### 注意事项

- jj 命令会频繁自动 import/export，可能导致分支冲突
- 大型仓库中 jj 会变慢（每次命令都执行 git import）
- 有冲突文件时 Git 工具可能出问题

## Multiple Remotes（多远程）

### 典型工作流

#### Fork 工作流（贡献上游）

```bash
# 1. 配置同时从多个 remote 拉取
jj config set --repo git.fetch '["upstream", "origin"]'

# 2. 推送只用 origin
jj config set --repo git.push origin

# 3. 跟踪远程 bookmark
jj bookmark track main  # 跟踪 origin/main
jj bookmark track main --remote=upstream  # 也跟踪 upstream

# 4. 设置 trunk（作为 immutable 基础）
jj config set --repo 'revset-aliases."trunk()"' main@upstream
```

#### 集成工作流（独立仓库）

```bash
# 1. 只从 origin 拉取和推送
jj config set --repo git.fetch '["origin"]'

# 2. 只跟踪 origin
jj bookmark track main --remote=origin
jj bookmark untrack main --remote=upstream

# 3. 设置 trunk 为 origin
jj config set --repo 'revset-aliases."trunk()"' main@origin
```

### Remote Bookmarks 引用

```bash
# 引用远程 bookmark
main@origin   # origin 上的 main
main@upstream # upstream 上的 main

# 在新远程上创建
jj new main@upstream
```

## Divergent Changes（分叉变化）

当同一 change ID 有多个可见 commit 时发生。

### 原因

1. 本地和远程同时修改了同一个 change
2. 从不同 workspace 操作同一 change
3. 并发操作导致

### 识别

```bash
jj log
# 显示：
# mzvwutvl/0 ... (divergent)
# mzvwutvl/1 ... (divergent)
```

### 解决策略

#### 1. 放弃一个

```bash
# 放弃不需要的版本
jj abandon <commit-id>
```

#### 2. 生成新 change ID

```bash
# 为一个 commit 生成新的 change ID
jj metaedit --update-change-id <commit-id>
```

#### 3. 合并内容

```bash
# 把一个 squash 到另一个
jj squash --from <source-commit-id> --into <target-commit-id>
```

#### 4. 忽略

如果不影响工作，可以暂时不管。

## Operation Log（操作日志）

jj 记录每次修改仓库的操作，比 Git 的 reflog 更强大。

### 查看

```bash
# 操作列表
jj op log

# 带 diff 的操作历史
jj op log -p
```

### 撤销

```bash
# 撤销上一次操作
jj undo

# 撤销到特定操作
jj undo --at-operation <operation-id>
```

### 恢复到之前状态

```bash
# 恢复整个仓库到某操作时的状态
jj op restore --at-operation <operation-id>
```

### 时光倒流

```bash
# 在某个操作的状态下运行命令（不修改）
jj --at-operation <operation-id> log
```

## Conflict 深入

### 冲突类型

1. **文件冲突**：同一文件同一位置被不同修改
2. **Bookmark 冲突**：本地和远程 bookmark 移动冲突
3. **Change 分叉**：同一 change ID 多个可见 commit

### 冲突解决

```bash
# 1. 创建新 commit 在冲突 commit 上
jj new <conflicted-commit>

# 2. 编辑文件解决冲突
# 编辑冲突标记...

# 3. 标记解决
jj resolve <file>

# 4. 如果有多个冲突文件，全部解决后
jj squash
```

### 冲突标记风格

可配置（默认 "diff"）：
```bash
# diff 风格（默认）
jj config set --user ui.conflict-marker-style diff

# snapshot 风格
jj config set --user ui.conflict-marker-style snapshot

# git 风格
jj config set --user ui.conflict-marker-style git
```

## Filesets（文件集）

类似 revset 但用于文件选择。

### 语法

```bash
# 文件路径
jj diff file.txt

# glob 模式
jj diff 'glob:*.rs'

# cwd 前缀
jj diff 'cwd:src/'

# root 前缀
jj diff 'root:src/'

# 组合
jj diff 'src ~ glob:**/test*.rs'
jj diff 'glob:*.rs | glob:*.md'
```

### 使用场景

```bash
# 拆分时只选部分文件
jj split 'glob:*.rs'

# 查看特定目录差异
jj diff 'root:src/'
```

## 配置示例

### 用户配置

```toml
[user]
name = "Your Name"
email = "your@email.com"

[ui]
color = "auto"
default-command = ["log", "--reversed"]

[diff]
color-words.max-inline-alternation = 3
```

### 自动签名

```toml
[signing]
behavior = "inline"
```
