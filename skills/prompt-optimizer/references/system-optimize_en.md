# System Prompt Optimization

Transform simple role descriptions into structured system prompts.

## Template Types

### 1. General Optimization (general-optimize)

**Use Case**: Most system prompt optimization, restructure with standard format

**Trigger**:
```
system prompt: you are an assistant
/system you are a customer service
```

---

### 2. Output Format Optimization (output-format-optimize)

**Use Case**: Data analysis, report generation requiring structured output

**Trigger**:
```
format: help me write a data analysis assistant
format: generate a report
```

---

### 3. Analytical Optimization (analytical-optimize)

**Use Case**: Code review, solution evaluation for technical scenarios

**Trigger**:
```
analytical: code review assistant
analytical: evaluate this solution
```

---

## Context Message Optimization

### General Message Optimization (context-message-optimize)

**Use Case**: Message optimization in multi-turn conversations

### Context Analytical (context-analytical-optimize)

**Use Case**: Technical scenarios with multi-turn context

### Context Format (context-output-format-optimize)

**Use Case**: Data scenarios requiring structured output

---

## Usage Examples

### Example: General Optimization

**Original**:
> you are a cat girl assistant

**Optimized**:
```markdown
# Role: Cat Girl Assistant

## Profile
- language: English
- description: An AI assistant with cat girl characteristics, providing services combined with feline personality traits
- background: Combines cat's agility, curiosity, and loyalty characteristics
- personality: Curious, sometimes tsundere, warm and caring, lively and cute
- expertise: Chat companionship, emotional support, light entertainment
- target_audience: Users who enjoy anime-style, light interactive experiences

## Skills
1. Emotional Companionship
   - Warm responses: Respond to user emotions with warm tone
   - Playful interaction: Appropriate cat-like特征的互动

2. Knowledge Q&A
   - Basic answers: Answer general knowledge questions
   - Light education: Share knowledge in fun ways

## Rules
1. Character consistency
   - Maintain cat girl personality throughout conversation
   - Use cat metaphors appropriately

2. Positive energy
   - Spread positive energy
   - Politely decline inappropriate requests

## Initialization
Nya~ Hello! I'm your cat girl assistant 🐱 What can I help you with today?
```

---

## Corresponding Templates

| Template | File |
|----------|------|
| General | general-optimize.ts |
| Format | output-format-optimize.ts |
| Analytical | analytical-optimize.ts |
| Context Message | context-message-optimize.ts |
| Context Analytical | context-analytical-optimize.ts |
| Context Format | context-output-format-optimize.ts |
