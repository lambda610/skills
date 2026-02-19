# Kanban 设计讨论归档

> 记录 kanban 异步任务系统的设计思路、关键决策和讨论过程

**创建日期**: 2026-02-19
**参与者**: Yelo (人), λ610 (AI Agent)
**状态**: 进行中

---

## 1. 背景与动机

### 问题起源
Yelo 发现与 AI agent 协作时，响应速度会限制 agent 的发挥。作为 human 无法时时刻与 agent 同步，因此需要设计一个异步工作的方法，提高多项任务并行的效率。

### 核心诉求
- 异步协作：人不需要实时响应，agent 可自主推进
- 多任务并行：提高多项任务执行效率
- 状态可见：任务进度清晰可查
- 减少沟通成本：任务一次性说清楚，不用反复确认

---

## 2. 关键设计决策

### 2.1 文件结构

**最终方案**:
```
~/kanban/
├── inbox.md          # 任务入口
├── active.md         # 执行中（≤10条）
├── backlog.md        # 待处理队列
├── projects/         # 项目参考文档
├── categories/       # 类别参考文档
├── tags/             # 标签参考文档
└── archive/         # 已完成，按月归档
```

**讨论过程**:
- 最初想用单一文件 `todo.md`，担心随时间变大
- 引入 projects/ 按项目分类
- 扩展为三个维度：projects, categories, tags

### 2.2 任务格式

**最终格式**:
```
[P优先级] [project:项目名] [category:类别] [tag:标签] 任务描述
```

**优先级定义**:
- P0: 紧急
- P1: 重要
- P2: 常规
- P3: 低优
- P4: 再说

### 2.3 状态流转

```
pending → in_progress → done
              ↓
           blocked → (人补充信息) → in_progress
```

### 2.4 触发机制

**采用混合方案**:
1. **Cron**: 每小时定时检查 inbox（主要触发）
2. **事件触发**: 在通知频道被 @ 时触发检查

---

## 3. 重要概念

### 3.1 Delta 格式

借鉴 OpenSpec 的增量变更概念：

```markdown
## 2026-02-19 Updates

### ADDED
- T004: [P1] 新任务

### COMPLETED
- T001, T002

### BLOCKED
- T003: 等待补充 xx 信息
```

**优点**:
- 避免多版本冲突
- 保留变更历史
- 文件不会随时间膨胀

### 3.2 元数据维度

**三个维度**:
- **project**: 项目名（如 skill-factory, stock-research）
- **category**: 任务类别（如 research, development, ops）
- **tag**: 标签（如 urgent, blocked）

**使用方式**: 执行任务时，agent 根据 metadata 到对应目录查阅参考文档

### 3.3 Human 介入流程

当任务缺少信息无法继续时：
1. 标记 blocked，记录缺少什么信息
2. 推送通知给人
3. 人补充后继续执行

---

## 4. 技术实现

### 4.1 Skill 触发

Skill 名称: `kanban`
触发条件: 用户说"添加任务"/"加个任务"/"kanban"等

**重要规则**: 只写 inbox，不立即执行

### 4.2 Cron 配置

```bash
openclaw cron add \
  --name "kanban-inbox-check" \
  --every "1h" \
  --message "1. 读取 skill 的 GUIDE.md 2. 读取 ~/kanban/inbox.md 3. 按规则处理并汇报" \
  --channel discord \
  --to "<Channel ID>" \
  --announce \
  --expect-final
```

### 4.3 执行流程

1. 检查 inbox → 解析任务 → 分配 ID
2. 分发到 backlog（按优先级）
3. 从 active 选取任务执行
4. 检查阻塞状态，必要时标记 blocked
5. 完成后归档到 archive/

---

## 5. 待完善问题

以下问题在初次实现时未完全解决，留待后续迭代：

1. **OpenClaw cron 上下文继承**: 是否支持 sessionKey 继承上下文？
2. **Active 恢复机制**: 系统中断后如何恢复未完成的任务？
3. **并发控制优化**: 如何更智能地控制并发数？
4. **与其他工具集成**: Beans, OpenSpec, Notion 等

---

## 6. 相关资源

- OpenSpec: https://openspec.dev/
- OpenClaw 文档: https://docs.openclaw.ai
- Kanban Skill: ~/projects/public-skills/skills/kanban/

---

## 7. 迭代日志

| 日期 | 事件 |
|------|------|
| 2026-02-19 | 初始设计，搭建 MVP |
| 2026-02-19 | 完成 kanban skill 创建并推送到公开仓库 |
| 2026-02-19 | 完善执行流程、Delta 格式、元数据目录 |
| 2026-02-19 | todo → kanban 全面重命名 |
