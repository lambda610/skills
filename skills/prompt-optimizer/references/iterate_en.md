# Iteration Optimization

Improve existing prompts based on new requirements.

## Core Concept

Iteration optimization is NOT re-optimization from scratch, but making incremental improvements to EXISTING optimized results based on new requirements.

## Template Types

### 1. General Iteration (iterate)

**Use Case**: Improve existing prompts based on specific issues and requirements

**Trigger**:
```
iterate:
original prompt: you are a customer service assistant
improvement: make output more concise
```

---

### 2. Context Iteration (context-iterate)

**Use Case**: Iteration within multi-turn conversation contexts

**Trigger**:
```
context iterate:
previous prompt: xxx
new requirement: xxx
```

---

### 3. Image Iteration (image-iterate-general)

**Use Case**: Progressive improvement of image prompts

**Trigger**:
```
image iterate:
previous result: xxx
improvement: add more details
```

---

## Core Principles

### Do ✅

- Keep the core intent of the original prompt
- Integrate improvement requirements appropriately
- Maintain original language style
- Make precise changes, avoid over-adjustment

### Don't ❌

- Don't misunderstand as directly executing requirements
- Don't significantly restructure
- Don't change core functionality

---

## Examples

### Example 1: General Iteration

**Original Prompt**:
> You are a customer service assistant, help users solve problems

**Improvement Requirement**:
> No interaction needed

**✅ Correct Result**:
> You are a customer service assistant, help users solve problems. Please provide complete solutions directly without multi-round interaction confirmations.

**❌ Wrong Interpretation**:
> OK, I won't interact with you

---

### Example 2: Format Adjustment

**Original Prompt**:
> Analyze data and give suggestions

**Improvement Requirement**:
> Output in JSON format

**✅ Correct Result**:
> Analyze data and give suggestions, please output analysis results in JSON format

---

### Example 3: Style Adjustment

**Original Prompt**:
> You are a writing assistant

**Improvement Requirement**:
> Make it more professional

**✅ Correct Result**:
> You are a professional writing consultant with rich writing experience, capable of providing professional writing guidance, copy optimization, and content improvement suggestions.

---

## Workflow

1. **Analyze original prompt** - Understand core functionality and structure
2. **Understand improvement requirement** - Add functionality? Modify approach? Add constraints?
3. **Integrate appropriately** - Blend requirement into original prompt
4. **Output complete** - Maintain original format, output complete modified version

---

## Corresponding Templates

| Template | File |
|----------|------|
| General Iteration | iterate.ts |
| Context Iteration | context-iterate.ts |
| Image Iteration | image-iterate-general.ts |
