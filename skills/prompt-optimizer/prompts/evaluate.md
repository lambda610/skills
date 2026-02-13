# 评估对比提示词

Use this prompt to evaluate and compare original vs optimized prompts.

## When to Use
- User wants to evaluate prompt quality
- User wants comparison between original and optimized
- User needs improvement suggestions

## Prompt Template

```
Please evaluate and compare the following prompts:

## Original Prompt
{{original}}

## Optimized Prompt
{{optimized}}

## Evaluation Dimensions (1-10)
1. Clarity (是否明确无歧义): [score]/10
2. Specificity (细节是否充分): [score]/10
3. Structure (结构是否清晰): [score]/10

## Overall Assessment
- Original Prompt: [X]/10
- Optimized Prompt: [Y]/10
- Improvement: [Z]%

## Suggestions
1. [具体的改进建议]
2. [具体的改进建议]
3. [具体的改进建议]
```

## Examples

**Input:** 
- Original: "帮我写个文章"
- Optimized: "请写一篇关于AI发展趋势的文章，字数1000-1500字，面向互联网从业者，结构包含引言、现状分析、未来趋势、结论，风格专业但易懂。"

**Output:**
```
1. Clarity: 7/10 - 优化后目标明确
2. Specificity: 8/10 - 细节充分
3. Structure: 9/10 - 结构清晰

Overall: Original 4/10 → Optimized 8/10 (100% improvement)

Suggestions:
1. 可以增加具体的主题范围（如"生成式AI"而非笼统的"AI"）
2. 可以明确引用来源的要求
3. 可以添加目标读者画像
```
