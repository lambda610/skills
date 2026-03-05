# 命令对照表（带解释）

> 基于官方文档：https://www.jj-vcs.dev/latest/git-command-table/

## 基础操作

| Git | Jujutsu | 说明 |
|-----|---------|------|
| `git status` | `jj st` | 查看当前工作状态 |
| `git diff` | `jj diff` | 查看未提交的修改 |
| `git diff HEAD` | `jj diff` | 同上，jj 默认比较 HEAD |
| `git diff <A>..<B>` | `jj diff -r A..B` | 比较两个提交 |
| `git add` | ❌ 不需要 | jj 自动追踪所有修改 |
| `git commit` | `jj commit -m "msg"` | 提交当前所有变更 |
| `git commit -a` | `jj commit` | 同上，jj 不需要 -a |
| `git commit --amend` | `jj squash` | 把当前变更合并到父提交 |
| `git restore <file>` | `jj restore <file>` | 撤销文件修改 |
| `git checkout -- <file>` | `jj restore <file>` | 同上 |

## 历史查看

| Git | Jujutsu | 说明 |
|-----|---------|------|
| `git log` | `jj log` | 查看历史 |
| `git log --oneline` | `jj log -r ::@` | 简洁格式 |
| `git log --graph` | `jj log --graph` | 图形化 |
| `git log --all` | `jj log -r 'all()'` | 查看所有 |
| `git show <rev>` | `jj show <rev>` | 查看提交详情 |
| `git blame <file>` | `jj file annotate <file>` | 文件注解 |

## ⚠️ 分支操作（关键区别！）

| Git | Jujutsu | 说明 |
|-----|---------|------|
| `git checkout <branch>` | `jj new <bookmark>` | **没有 jj co!** |
| `git checkout -b <name>` | `jj new <base> -b <name>` | 创建并切换 |
| `git branch` | `jj bookmark list` | 列出 |
| `git branch <name>` | `jj bookmark create <name>` | 创建 |
| `git branch -d <name>` | `jj bookmark delete <name>` | 删除 |
| `git branch -f <name> <rev>` | `jj bookmark move <name> --to <rev>` | 移动 |

**关键点**：
- jj 没有 `jj co` 或 `jj checkout` 命令！
- 用 `jj new <bookmark>` 创建新 change 并切换到它
- 用 `jj edit <revision>` 在 working copy 中编辑某 commit

## 变基与合并

| Git | Jujutsu | 说明 |
|-----|---------|------|
| `git merge <A>` | `jj new @ A` | 合并（创建新 change） |
| `git rebase <B> <A>` | `jj rebase -b A -o B` | 移动 bookmark |
| `git rebase --onto B A^ <branch>` | `jj rebase -s A -o B` | 移动 commit 及后代 |

**关键区别**：
- `-b` = 移动 bookmark 指向的 commit（不包含后代）
- `-s` = 移动指定 commit 及其所有后代

## 远程操作

| Git | Jujutsu | 说明 |
|-----|---------|------|
| `git fetch` | `jj git fetch` | 拉取 |
| `git pull` | `jj git fetch` (+ `jj new`) | |
| `git push` | `jj git push` | 推送 |
| `git push <remote> <branch>` | `jj git push --bookmark <name>` | |
| `git remote add` | `jj git remote add` | |
| `git branch -u <remote>/<branch>` | `jj bookmark track <name> --remote=<remote>` | 跟踪远程 |

## 暂存与撤销

| Git | Jujutsu | 说明 |
|-----|---------|------|
| `git stash` | `jj new @-` | 暂存到兄弟 commit |
| `git stash pop` | `jj edit <commit>` | 恢复 |
| `git reset --hard` | `jj abandon` | 放弃当前 change |
| `git reset --soft HEAD~` | `jj squash --from @-` | 保留修改 |
| `git cherry-pick <rev>` | `jj duplicate <rev> -o @` | 复制提交 |

## 撤销操作

| Git | Jujutsu | 说明 |
|-----|---------|------|
| `git reflog` | `jj op log` | 查看操作日志 |
| `git reset --hard <ref>` | `jj undo` | 撤销上一次操作 |

**jj 的 `jj undo` 更强大** — 可以撤销几乎任何操作！

## 文件操作

| Git | Jujutsu | 说明 |
|-----|---------|------|
| `git ls-files` | `jj file list` | 列出文件 |
| `git rm <file>` | `jj file delete <file>` | 删除 |
| `git rm --cached <file>` | `jj file untrack <file>` | 取消跟踪（需匹配 ignore pattern） |
| `git rev-parse --show-toplevel` | `jj workspace root` | 仓库根目录 |

## 高级操作

| Git | Jujutsu | 说明 |
|-----|---------|------|
| `git add -p` | `jj split` | 交互式拆分 |
| `git rebase -i` | `jj rebase -r` | 交互式变基 |
| | `jj absorb` | 自动吸收修改到之前的 commit |
| | `jj diffedit` | 交互式编辑某 commit 的 diff |
| | `jj describe` | 修改 commit 信息 |
| | `jj evolog` | 查看 change 的演化历史 |
