# Revset 查询语法

> 基于官方文档：https://www.jj-vcs.dev/latest/revsets/

Revset 是 jj 强大的查询语法，能精确定位提交。

## 基本语法

```bash
jj log -r <revset>
```

## 常用符号

| 符号 | 含义 |
|------|------|
| `@` | 当前 working-copy commit |
| `@-` | 当前 commit 的父提交 |
| `@--` | 祖父提交 |
| `main` | bookmark 名为 main 的提交 |
| `HEAD` | HEAD 指向的提交 |
| `root()` | 仓库根提交（虚拟 commit，hash 全为 0） |

## 运算符

| 运算符 | 含义 | 示例 |
|--------|------|------|
| `::` | 祖先范围（包含自己） | `main::` = main 的所有后代 |
| `..` | 不包含祖先 | `main..main~5` |
| `|` | 并集 | `main \| feature` |
| `&` | 交集 | `main & @` |
| `~` | 差集 | `@ ~ main` |
| `-` | 父母（单数） | `@-` = 父提交 |
| `+` | 子孙（单数） | |

## 范围运算符

| 运算符 | 含义 |
|--------|------|
| `x::y` | x 到 y 之间的后代（包含 x 和 y） |
| `x..y` | x 到 y 之间的祖先（不包含 x 的祖先） |
| `::x` | x 的所有祖先 |
| `x::` | x 的所有后代 |

**注意**：`..` 在左边时不分配（不同于 `|`）：
- `(A | B)..` = `A.. & B..`（交集）
- `A.. | B..` = 并集

## 函数

| 函数 | 用法 | 说明 |
|------|------|------|
| `all()` | `all()` | 所有可见 commit |
| `none()` | `none()` | 空集 |
| `bookmarks()` | `bookmarks()` | 所有本地 bookmark |
| `bookmarks(pattern)` | `bookmarks("main")` | 匹配 pattern 的 bookmark |
| `remote_bookmarks()` | `remote_bookmarks()` | 所有远程 bookmark |
| `visible_heads()` | `visible_heads()` | 所有可见 head |
| `parents(x)` | `parents(@)` | x 的父母 |
| `children(x)` | `children(@)` | x 的子孙 |
| `ancestors(x)` | `ancestors(@)` | x 的祖先 |
| `descendants(x)` | `descendants(@)` | x 的后代 |
| `first_parent(x)` | `first_parent(@)` | 只取第一个父母 |
| `latest(x)` | `latest(@, 5)` | 最近 N 个 |
| `merges()` | `merges()` | 合并提交 |
| `file(path)` | `file("src/main.rs")` | 包含某文件的 commit |
| `author(name)` | `author("yelo")` | 作者匹配 |
| `description(text)` | `description("feat")` | 描述包含 |
| `date(expr)` | `date(2024-01-01)` | 日期 |

## 常见用法

```bash
# 当前分支的历史
jj log -r ::@

# 所有未推送的提交
jj log -r '@..@|bookmarks(@)..'

# 某个 bookmark 的历史
jj log -r main::main

# 最近 5 个提交
jj log -r latest(@, 5)

# 包含某个文件的提交
jj log -r 'file(path/to/file)'

# 在某日期之后的提交
jj log -r 'date(2024-01-01)..'

# 作者包含某字符串的提交
jj log -r 'author(yelo)'

# 合并提交
jj log -r 'merges()'

# 空提交（无文件变更）
jj log -r 'empty()'

# 可变 commits（本地修改过的）
jj log -r 'mutable()'
```

## 快捷方式

| 快捷 | 展开 |
|-------|------|
| `@~n` | `@-n`，第 n 个祖先 |
| `@^` | `@-`，父提交 |
| `main~3` | main 的第 3 个祖先 |

## 示例

```bash
# 查看当前 commit 的祖先链
jj log -r ::@

# 查看 feature 分支独有的提交
jj log -r 'feature - main'

# 查看最近一周的提交
jj log -r 'date(-7d)..'

# 查看两个 bookmark 之间的差异
jj diff -r main..feature

# 查看某个人的所有提交
jj log -r 'author(yelo)'

# 查看所有 bookmark 的最新位置
jj log -r 'bookmarks()'
```
