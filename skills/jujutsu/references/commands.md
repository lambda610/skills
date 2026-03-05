# 命令对照表（带解释）

> 对比 Git 命令，理解为什么不同。

## 基础操作

| Git | Jujutsu | 说明 |
|-----|---------|------|
| `git status` | `jj st` | 查看当前工作状态 |
| `git diff` | `jj diff` | 查看未提交的修改 |
| `git diff HEAD` | `jj diff` | 同上，jj 默认比较 HEAD |
| `git diff <A>..<B>` | `jj diff -r <A> --to <B>` | 比较两个提交 |
| `git add` | ❌ 不需要 | jj 自动追踪所有修改 |
| `git commit` | `jj commit -m "msg"` | 提交当前所有变更 |
| `git commit -a` | `jj commit` | 同上，jj 不需要 -a |
| `git commit --amend` | `jj squash @` | 把变更合并到当前提交 |
| `git restore <file>` | `jj restore <file>` | 撤销文件修改 |
| `git checkout -- <file>` | `jj restore <file>` | 同上 |

## 历史查看

| Git | Jujutsu | 说明 |
|-----|---------|------|
| `git log` | `jj log` | 查看历史（默认显示当前 change） |
| `git log --oneline` | `jj log -r ::@` | 简洁格式 |
| `git log --graph` | `jj log --graph` | 图形化（jj 更美观） |
| `git log --all` | `jj log -r 'all()'` | 查看所有 bookmark |
| `git show <rev>` | `jj show <rev>` | 查看提交详情 |
| `git blame <file>` | `jj file annotate <file>` | 查看文件每行最后修改 |

## 分支操作（Bookmarks）

| Git | Jujutsu | 说明 |
|-----|---------|------|
| `git branch` | `jj bookmark list` | 列出分支 |
| `git branch <name>` | `jj bookmark create <name>` | 创建分支 |
| `git branch -d <name>` | `jj bookmark delete <name>` | 删除分支 |
| `git checkout <name>` | `jj co <name>` | 切换分支 |
| `git checkout -b <name>` | `jj new <name>` | 创建并切换 |
| `git branch -f <name> <rev>` | `jj bookmark move <name> --to <rev>` | 移动分支 |

**注意**：jj 的 bookmarks 是轻量指针，不是 Git branch 的完全等价物。

## 变基与合并

| Git | Jujutsu | 说明 |
|-----|---------|------|
| `git merge <A>` | `jj new @ <A>` | 合并（创建新 change） |
| `git rebase <B> <A>` | `jj rebase -b <A> -o <B>` | 变基 |
| `git rebase --onto B A^ <branch>` | `jj rebase -s A -o B` | 变基到新基础 |
| `git rebase -i` | `jj rebase -r` | 交互式变基 |

## 远程操作

| Git | Jujutsu | 说明 |
|-----|---------|------|
| `git fetch` | `jj git fetch` | 拉取 |
| `git pull` | `jj git fetch` (+ `jj new`) | 拉取后创建新 change |
| `git push` | `jj git push` | 推送 |
| `git push <remote> <branch>` | `jj git push --bookmark <name>` | 推送特定 bookmark |
| `git remote add <name> <url>` | `jj git remote add <name> <url>` | 添加远程 |

## 暂存与撤销

| Git | Jujutsu | 说明 |
|-----|---------|------|
| `git stash` | `jj shelf` | 暂存当前变更 |
| `git stash pop` | `jj shelf unapply` | 恢复暂存 |
| `git reset --hard` | `jj abandon` | 放弃当前 change |
| `git reset --soft HEAD~` | `jj squash --from @-` | 保留修改并新建 change |
| `git cherry-pick <rev>` | `jj duplicate <rev> -o @` | 复制提交 |

## 撤销操作

| Git | Jujutsu | 说明 |
|-----|---------|------|
| `git reflog` | `jj op log` | 查看操作日志 |
| `git reset --hard <ref>` | `jj undo` | 撤销上一次操作 |

**jj 的 `jj undo` 比 Git 的 reset 更强大**，可以撤销几乎任何操作。

## 文件操作

| Git | Jujutsu | 说明 |
|-----|---------|------|
| `git ls-files` | `jj file list` | 列出跟踪的文件 |
| `git rm <file>` | `jj file delete <file>` | 删除文件 |
| `git rm --cached <file>` | `jj file untrack <file>` | 取消跟踪 |
| `git rev-parse --show-toplevel` | `jj workspace root` | 仓库根目录 |
