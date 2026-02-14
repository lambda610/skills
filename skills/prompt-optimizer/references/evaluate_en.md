# Prompt Evaluation

Evaluate prompt quality with multi-dimensional scoring and improvement suggestions.

## Evaluation Modes

### By Evaluation Target

| Mode | Description | Use Case |
|------|-------------|----------|
| Original Evaluation | Evaluate original prompt | Understand baseline quality |
| Optimized Evaluation | Evaluate optimized prompt | Verify optimization effect |
| Comparison | Original vs Optimized | Quantify improvement |

### By Evaluation Method

| Mode | Description | Needs Test Result |
|------|-------------|-------------------|
| Direct | Evaluate quality directly | ❌ No |
| Iterative | Evaluate + improvement plan | ❌ No |
| Comparison | Original vs Optimized | ✅ Yes |

### By Prompt Type

- **System Prompt Evaluation**
- **User Prompt Evaluation**  
- **Multi-message Conversation Evaluation**
- **Variable Mode Evaluation**
- **Image Prompt Evaluation**

---

## Evaluation Dimensions

### Basic Dimensions (1-10 points)

1. **Clarity**
   - Any ambiguity?
   - Is the goal clear?

2. **Specificity**
   - Are details sufficient?
   - Are constraints clear?

3. **Structure**
   - Is the format clear?
   - Is the logic coherent?

---

## Trigger Methods

### Comparison Evaluation
```
evaluate:
original prompt: write an article for me
optimized prompt: xxx
```

### Direct Evaluation
```
evaluate this prompt: write an article for me
```

### Iterative Evaluation
```
iterative evaluation:
prompt: xxx
```

---

## Output Format

### Direct Evaluation Output

```markdown
## Evaluation Result

| Dimension | Score | Notes |
|-----------|-------|-------|
| Clarity | 8/10 | Goal is clear |
| Specificity | 7/10 | Details insufficient |
| Structure | 9/10 | Good format |

**Total**: 8/10

## Improvement Suggestions

1. [Specific suggestion]
2. [Specific suggestion]
```
