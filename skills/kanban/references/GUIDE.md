# Kanban 异步任务系统

> 轻量级异步任务管理方法，配合 OpenClaw 使用

**⚠️ 注意**：这是一个轻量级 skill，不包含安装脚本。需要手动配置目录和 cron（见下方安装配置章节）。

---

## 核心理念

- **异步协作**：人不需要实时响应，agent 可自主推进
- **多任务并行**：提高多项任务执行效率
- **状态可见**：任务进度清晰可查

---

## 文件结构

```
~/todo/                    # 任务数据目录
├── inbox.md              # 任务入口
├── active.md             # 执行中（≤10条）
├── backlog.md            # 待处理队列
├── projects/             # 按项目分类
└── archive/              # 已完成，按月归档
```

---

## 触发机制

### 1. Cron 定时检查（推荐）
```
每 1 小时检查一次 ~/todo/inbox.md
```

### 2. 事件触发
```
在任务汇报频道被 @ 时触发检查
```

---

## 执行流程

### 1. 检查 inbox
- 读取 inbox.md
- 解析新任务（优先级、项目）
- 分配任务 ID

### 2. 分发任务
- P0 → 立即处理，进 active
- P1 → 进 active 或 backlog
- P2/P3/P4 → 进 backlog

### 3. 执行任务
- 检查前置依赖（depends-on）
- 更新状态：in_progress
- 完成后标记 done，移入 archive
- 卡住标记 blocked

### 4. 汇报
- 做完推送到通知频道
- 定期汇总进度

---

## 状态流转

```
pending → in_progress → done
              ↓
           blocked → (等待确认) → in_progress
```

---

## 任务格式

### inbox 格式
```
[P优先级] [项目名] 任务描述
```

### active 格式
```markdown
- [in_progress] T001: [P1] [project] 任务描述
  - owner: agent-name
  - depends-on: T000
  - updated: YYYY-MM-DD
```

---

## 优先级

- P0: 紧急
- P1: 重要
- P2: 常规
- P3: 低优
- P4: 再说

---

## 配置说明

### 通知频道
根据你的平台选择：
- Discord: 使用 channel ID
- Telegram: 使用 chat ID

### Cron 频率
根据需要调整：
- 每小时: `every 1h`
- 每 30 分钟: `every 30m`

---

## 安装配置（手动）

由于 kanban 是轻量级任务管理方法，不需要安装额外组件，只需：

### 步骤 1：创建本地任务目录

```bash
mkdir -p ~/todo/{projects,archive}
```

### 步骤 2：创建基础文件

从 `references/templates/` 复制模板文件到 `~/todo/`：

```bash
# 复制模板文件
cp ~/projects/public-skills/skills/kanban/references/templates/inbox.md ~/todo/
cp ~/projects/public-skills/skills/kanban/references/templates/active.md ~/todo/
cp ~/projects/public-skills/skills/kanban/references/templates/backlog.md ~/todo/

# 创建 archive 目录的说明文件
echo "# Archive 归档" > ~/
```

### todo/archive/README.md步骤 3：配置 Cron

参考下方的配置示例，根据你的平台调整：

**Discord 示例**：
```bash
openclaw cron add \
  --name "kanban-inbox-check" \
  --every "1h" \
  --message "1. 读取 ~/projects/public-skills/skills/kanban/references/README.md 了解执行规则 2. 读取 ~/todo/inbox.md 检查是否有新任务 3. 按规则处理并汇报到 <你的Channel ID>" \
  --channel discord \
  --to "<你的Channel ID>" \
  --announce \
  --expect-final
```

**Telegram 示例**：
```bash
openclaw cron add \
  --name "kanban-inbox-check" \
  --every "1h" \
  --message "1. 读取 ~/projects/public-skills/skills/kanban/references/README.md 了解执行规则 2. 读取 ~/todo/inbox.md 检查是否有新任务 3. 按规则处理并汇报到 <你的Chat ID>" \
  --channel telegram \
  --to "<你的Chat ID>" \
  --announce \
  --expect-final
```

### 步骤 4：通知频道

- 创建一个专属频道用于接收任务汇报（如 #kanban）
- 将频道 ID 填入上方配置中的 `<你的Channel ID>`

---

## 验证安装

配置完成后，可以手动触发一次测试：

```bash
# 往 inbox 添加测试任务
echo "[P2] 测试任务" >> ~/todo/inbox.md

# 手动触发 cron
openclaw cron run <job-id>
```

或者直接在频道 @ 你的 agent 说"检查 todo"。

---

## OpenClaw Cron 配置示例

```bash
# 每小时检查 inbox
openclaw cron add \
  --name "todo-inbox-check" \
  --every "1h" \
  --message "1. 读取 ~/todo/README.md 了解执行规则 2. 读取 ~/todo/inbox.md 检查是否有新任务 3. 按规则处理任务并汇报进度到 <通知频道ID>" \
  --channel <discord/telegram> \
  --to "<通知频道ID>" \
  --announce \
  --expect-final
```

---

## 进阶用法

### 按项目分类
在 `projects/` 目录下创建项目文件：
```
projects/
├── skill-factory.md
└── stock-research.md
```

### Delta 更新
不每次重写全量，用 delta 格式标记变更：
```markdown
## 2026-02-19 Updates

### ADDED
- T004: [P1] 新任务

### COMPLETED
- T001, T002
```

---

## 相关资源

- OpenClaw 文档: https://docs.openclaw.ai
- Skill: `kanban` (在公开 skills 仓库)
