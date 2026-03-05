# Revset 查询语法

Revset 是 jj 强大的查询语法，能精确定位提交。

## 基本语法

```bash
jj log -r <revset>
```

## 常用查询

| Revset | 含义 |
|--------|------|
| `@` | 当前工作 change |
| `@-` | 当前 change 的父提交 |
| `@--` | 祖父提交 |
| `main` | bookmark 名为 main 的提交 |
| `HEAD` | HEAD 指向的提交 |
| `root` | 仓库根提交 |

## 运算符

| 运算符 | 含义 | 示例 |
|--------|------|------|
| `::` | 祖先范围 | `main::` = main 的所有后代 |
| `..` | 包含范围 | `main..main~5` |
| `|` | 并集 | `main | feature` |
| `&` | 交集 | `main & @` |
| `-` | 差集 | `@ - main` |
| `+` | 并集（同 `\|`） | |
| `::` | 子孙 | `A::B` = A 到 B 之间的提交 |

## 常见用法

```bash
# 当前分支的历史
jj log -r @::@-

# 所有未推送的提交
jj log -r '@..@|bookmarks(@)..'

# 某个 bookmark 的历史
jj log -r main::main

# 最近 5 个提交
jj log -r @--..

# 包含某个文件的提交
jj log -r "file(path/to/file)"

# 在某日期之后的提交
jj log -r "date(2024-01-01).."

# 作者包含某字符串的提交
jj log -r "author(yelo)"
```

## 谓词

| 谓词 | 用法 | 说明 |
|------|------|------|
| `date()` | `date(2024-01-01)` | 日期 |
| `author()` | `author(yelo)` | 作者 |
| `committer()` | `committer(bot)` | 提交者 |
| `file()` | `file(src/main.rs)` | 包含某文件 |
| `description()` | `description(feat)` | 描述包含 |
| `empty()` | `empty()` | 空提交（无文件变更） |
| `public()` | `public()` | 已推送的提交 |

## 快捷方式

| 快捷 | 展开 |
|-------|------|
| `@~n` | `@-n`，即第 n 个祖先 |
| `@^` | `@-`，即父提交 |
| `main~3` | main 的第 3 个祖先 |

## 示例

```bash
# 查看当前 change 的祖先链
jj log -r @::@-

# 查看 feature 分支独有的提交
jj log -r "feature - main"

# 查看最近一周的提交
jj log -r "date(-7d).."

# 查看两个 bookmark 之间的差异
jj diff -r main..feature
```
