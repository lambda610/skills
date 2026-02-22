---
name: kanban
description: "异步任务管理系统。用于：(1) 添加任务到 inbox，(2) 查看任务进度，(3) 处理 backlog。触发方式：用户说'添加任务'/'task add'/'kanban'或类似表达。注意：只写 inbox，不立即执行任务。Not for: 需要立即执行的任务。"
metadata: {"openclaw": {"emoji": "📋"}}
---

# Kanban Skill

异步任务管理系统，配合 `~/kanban/` 目录使用。

## 触发条件

用户说以下任一指令时触发：
- "添加任务"
- "加个任务"
- "task add"
- "帮我记个任务"
- "kanban"
- 或任何表达"添加任务到待办"的意图

## When to Use

- 用户说"添加任务"、"加个任务"、"task add"
- 用户说"帮我记个任务"
- 用户提到"kanban"或待办
- 需要异步处理的任务（不是立即执行）

## Prerequisites

- 本地 `~/kanban/` 目录已配置
- inbox.md、active.md、backlog.md 文件存在

## 执行规则

### 添加任务（只执行这个，不要执行任务本身！）

1. 解析任务信息：
   - 优先级：`[P0-P4]`，默认 P2
   - 项目名：`[project:xxx]`，可选
   - 类别：`[category:xxx]`，可选
   - 标签：`[tag:xxx]`，可选
   - 任务描述：具体做什么

2. 写入 `~/kanban/inbox.md`：
```
[P优先级] [project:项目名] [category:类别] [tag:标签] 任务描述
```

3. **重要**：只写 inbox，**不要立即执行任务**！等 cron 触发或用户主动要求检查时再处理。

4. 回复用户确认已添加。

### 查看进度

用户说"查看 kanban"/"任务进度"/"还有哪些任务"时：
- 读取 `~/kanban/active.md` 和 `~/kanban/backlog.md`
- 汇总当前状态汇报给用户

### Human 介入

任务执行中需要补充信息时：
- 标记 blocked
- 记录缺少什么信息
- 推送给人确认

## 文件结构

```
~/kanban/                    # 本地任务数据
├── inbox.md                # 任务入口
├── active.md               # 执行中
├── backlog.md              # 待处理
├── projects/               # 项目参考文档
├── categories/             # 类别参考文档
├── tags/                   # 标签参考文档
└── archive/                # 已完成

skill 目录:
kanban/
├── SKILL.md               # 触发规则
└── references/
    ├── GUIDE.md           # 完整使用文档
    └── templates/          # 模板文件
```

## 优先级

- P0: 紧急
- P1: 重要
- P2: 常规
- P3: 低优
- P4: 再说

## 示例

**用户说**："帮我加一个 P1 任务，研究 GPU 板块"

**执行**：
1. 写入 `~/kanban/inbox.md`：
```
[P1] [project:stock-research] 研究 GPU 板块
```
2. 回复："✅ 已添加到 inbox，等 cron 触发或你要求检查时我会处理。"

**用户说**："查看任务进度"

**执行**：
1. 读取 active.md 和 backlog.md
2. 汇总汇报当前状态
