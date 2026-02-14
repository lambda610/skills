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

## Guided Workflow / 引导式流程

If you need guidance, follow this interactive process:

### Step 1: Select Function / 选择功能
```
你想做什么？/ What would you like to do?
- 优化提示词 (Optimize a prompt)
- 评估提示词 (Evaluate a prompt)
- 生成图像提示词 (Generate image prompt)
```

### Step 2: Select Type / 选择类型 (Dynamic / 动态)

Based on selection, ask for specific type:

**用户提示词优化 / User Prompt Optimization:**
- 基础优化 (Basic)
- 规划优化 (Planning)
- 专业优化 (Professional)

**系统提示词优化 / System Prompt Optimization:**
- 通用优化 (General)
- 格式化优化 (Format)
- 分析型优化 (Analytical)

**图像优化 / Image Optimization:**
- 文生图 (Text-to-Image)
- 图生图 (Image-to-Image)

**迭代优化 / Iteration:**
- 通用迭代 (General)
- 图像迭代 (Image)

### Step 3: Input Prompt / 输入提示词
请提供需要优化的提示词 / Please provide the prompt to optimize

### Step 4: Additional Info (Dynamic) / 补充信息 (动态)

Ask based on template needs:

**用户提示词:**
- 目标模型: ChatGPT / Claude / 其他?
- 输出格式: Markdown / JSON / 纯文本?
- 长度限制: 有无字数要求?

**系统提示词:**
- 目标模型: 用于哪个 AI?
- 复杂度: 简单 / 详细 / 完整版?

**图像提示词 / Image Prompt:**
- 目标工具 / Target Tool: Midjourney / DALL-E / Stable Diffusion / FLUX / 即梦 (JM) / 其他
- 风格 / Style: 写实 / 摄影 / 插画 / 3D / 其他
- 画面比例 / Aspect Ratio: 1:1 / 16:9 / 9:16 / 其他
- 参考图 / Reference Image: 是 (Yes) / 否 (No)
  - 如果是: 参考图数量、具体约束（如：使用第一张图的产品）

**迭代优化:**
- 上次优化结果: [获取上次结果]
- 改进需求: [具体改进点]

### Step 5: Output / 输出优化结果

### Example / 示例流程
```
用户: 我想优化一个提示词
AI: 请问是哪种类型？
  1. 用户提示词（日常使用）
  2. 系统提示词（角色设定）
  3. 图像提示词（AI绘画）

用户: 3 (图像)
AI: 请选择：
  1. 文生图 (Text-to-Image)
  2. 图生图 (Image-to-Image)

用户: 1
AI: 请描述想要的图像

用户: 一个长发女性用直发夹，像沙宣广告
AI: 请问目标工具是什么？(可选)
  - Midjourney / DALL-E / Stable Diffusion / 其他

用户: Midjourney
AI: 请问风格偏好？(可选)
  - 写实 / 摄影 / 插画 / 3D

用户: 摄影
AI: [优化后...]
```

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
