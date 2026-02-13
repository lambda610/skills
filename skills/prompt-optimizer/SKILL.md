---
name: prompt-optimizer
description: "AI 提示词优化工具。支持：(1) 用户提示词优化，(2) 系统提示词优化，(3) 迭代改进，(4) 文生图/图生图提示词优化，(5) 质量评估对比。使用场景：优化模糊提示词、构建系统提示词、改进现有提示词、生成图像提示词、评估提示词质量。"
metadata:
  {
    "openclaw": {
      "emoji": "✨",
      "user-invocable": true
    }
  }
---

# Prompt Optimizer

AI 提示词优化工具，帮助编写高质量提示词。

## 快速开始

### 触发方式

**自动触发** - 描述需求即可：
```
优化：帮我写个文章
系统提示词：你是一个助手
/image 一只猫
评估：
原始提示词：xxx
优化后提示词：xxx
```

**命令触发** (OpenClaw)：
```
/prompt-optimizer optimize <需求>
/prompt-optimizer system <角色描述>
/prompt-optimizer image <图像描述>
/prompt-optimizer evaluate
```

## 功能概览

| 功能 | 触发关键词 | 说明 |
|------|----------|------|
| 用户提示词优化 | `优化：` | 模糊→清晰具体 |
| 系统提示词优化 | `/system` | 角色描述→结构化 |
| 迭代改进 | `迭代：` | 二次改进已有提示词 |
| 文生图优化 | `/image` | 自然语言→高质量图像提示词 |
| 评估对比 | `评估：` | 评分 + 改进建议 |

## 详细用法

### 用户提示词优化

详见 [references/user-optimize.md](references/user-optimize.md)

### 系统提示词优化

详见 [references/system-optimize.md](references/system-optimize.md)

### 质量评估

详见 [references/evaluate.md](references/evaluate.md)
