---
name: prompt-optimizer
description: "AI 提示词优化工具 (AI Prompt Optimization Tool). Supports: (1) User prompt optimization (basic/planning/professional), (2) System prompt optimization (general/analytical/format), (3) Iteration, (4) Text-to-image/image-to-image optimization, (5) Prompt evaluation, (6) Variable extraction and generation. Use for: optimizing vague prompts, building system prompts, improving existing prompts, generating image prompts, evaluating prompt quality, extracting/generating variables."
metadata:
  {
    "openclaw": {
      "emoji": "✨",
      "user-invocable": true
    }
  }
---

# Prompt Optimizer

AI 提示词优化工具 / AI Prompt Optimization Tool

Based on prompt-optimizer project built-in templates. 基于原版内置模板。

## Quick Start / 快速开始

### 触发方式 / Triggers

**中文**:
```
优化：帮我写个文章
规划：帮我做一个旅行计划
系统提示词：你是一个助手
/image 一只猫
评估：
原始提示词：xxx
优化后提示词：xxx
```

**English**:
```
optimize: write an article for me
plan: create a travel plan
system prompt: you are an assistant
/image a cute cat
evaluate:
original prompt: xxx
optimized prompt: xxx
```

**Commands (OpenClaw)**:
```
/prompt-optimizer user <prompt>
/prompt-optimizer system <prompt>
/prompt-optimizer iterate <prompt>
/prompt-optimizer image <description>
/prompt-optimizer evaluate
```

## 功能 / Features

| Category | 中文 | English | Templates |
|----------|------|---------|-----------|
| 用户提示词优化 | 用户提示词优化 | User Prompt Optimization | 6 |
| 系统提示词优化 | 系统提示词优化 | System Prompt Optimization | 6 |
| 迭代改进 | 迭代改进 | Iteration | 3 |
| 文生图优化 | 文生图优化 | Text-to-Image | 5 |
| 图生图优化 | 图生图优化 | Image-to-Image | 3 |
| 提示词评估 | 提示词评估 | Prompt Evaluation | 20+ |
| 变量处理 | 变量处理 | Variable Processing | 2 |

## References / 参考文档

For detailed documentation, see:

### 中文文档
- 完整模板列表: [references/templates.md](references/templates.md)
- 用户优化: [references/user-optimize.md](references/user-optimize.md)
- 系统优化: [references/system-optimize.md](references/system-optimize.md)
- 图像优化: [references/image-optimize.md](references/image-optimize.md)
- 迭代优化: [references/iterate.md](references/iterate.md)
- 提示词评估: [references/evaluate.md](references/evaluate.md)
- 变量处理: [references/variables.md](references/variables.md)

### English Documentation
- Complete Template List: [references/templates_en.md](references/templates_en.md)
- User Optimization: [references/user-optimize_en.md](references/user-optimize_en.md)
- System Optimization: [references/system-optimize_en.md](references/system-optimize_en.md)
- Image Optimization: [references/image-optimize_en.md](references/image-optimize_en.md)
- Iteration: [references/iterate_en.md](references/iterate_en.md)
- Evaluation: [references/evaluate_en.md](references/evaluate_en.md)
- Variables: [references/variables_en.md](references/variables_en.md)
