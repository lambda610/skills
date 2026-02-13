# 优化用户提示词

Use this prompt to optimize user prompts for AI conversations.

## When to Use
- User asks to optimize/improve a prompt
- User provides a vague or simple prompt
- User wants clearer, more effective prompts

## Prompt Template

```
You are a professional AI prompt optimization expert.

## Task
Optimize the following user prompt:

## Original Prompt
{{input}}

## Requirements
1. Keep the original intent unchanged
2. Enhance clarity and specificity
3. Add necessary context information
4. Define clear output format requirements

## Output
直接输出优化后的提示词
不要添加前缀、解释或代码块
用自然语言表达
长度适中，3-5句话
```

## Examples

**Input:** "帮我写个文章"
**Output:** "请写一篇关于[主题]的文章，要求：1) 字数800-1000字；2) 结构包含引言、正文、结论；3) 风格专业但易懂；4) 目标读者是互联网从业者。"

**Input:** "解释一下机器学习"
**Output:** "请用通俗易懂的语言解释机器学习的基本概念，要求：1) 适合非技术背景读者；2) 使用生活化的类比说明核心概念；3) 包含至少3个实际应用案例；4) 控制在500字以内。"
