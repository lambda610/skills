# User Prompt Optimization

Transform vague or simple prompts into clear, specific, and effective prompts.

## Template Types

### 1. Basic Optimization (user-prompt-basic)

**Use Case**: Quick daily optimization, eliminate vague expressions, add key information

**Trigger**:
```
optimize: write an article for me
basic: write a story
```

**Key Points**:
- Identify and replace vague words (e.g., "good" → specific description)
- Add missing key details
- Organize structure
- Clarify goals

---

### 2. Planning Optimization (user-prompt-planning)

**Use Case**: Complex tasks, break down vague requirements into actionable steps

**Trigger**:
```
plan: create a travel plan
stepwise: complete this task
```

**Key Points**:
- Intent recognition → core goal
- Task decomposition → subtasks
- Step ordering → execution sequence
- Detail addition → executability

---

### 3. Professional Optimization (user-prompt-professional)

**Use Case**: Scenarios requiring precise descriptions, add quantifiable standards

**Trigger**:
```
professional: help me process data
professional: write a report
```

**Key Points**:
- General → specific requirements
- Add quantifiable standards
- Define parameters and boundaries
- Clear acceptance criteria

---

### 4-6. Context Versions

**Trigger**:
```
context optimize: help me write code
context plan: build a system
context professional: handle this business
```

**Features**:
- Use in multi-turn conversation contexts
- Minimum sufficient refinement
- Clear scope, parameters, format, and acceptance criteria

---

## Usage Examples

### Example 1: Basic Optimization

**Original**:
> write an article for me

**Optimized**:
> Please write an article about AI technology development with these requirements:
> - 800-1000 words
> - For general audience
> - Include 3 real-world application examples
> - Engaging and interesting writing style

---

### Example 2: Planning Optimization

**Original**:
> create a travel plan

**Optimized**:
> # Task: Travel Plan
>
> ## 1. Role & Goal
> You are a professional travel planner, your core goal is to design a detailed 7-day travel itinerary.
>
> ## 2. Background & Context
> - Destination: [Please specify]
> - Duration: [Please specify]
> - Budget: [Please specify]
>
> ## 3. Key Steps
> 1. Research phase
> 2. Booking phase
> 3. Itinerary finalization
>
> ## 4. Output Requirements
> - Include: accommodation, food, transportation
> - Format: Markdown

---

## Corresponding Templates

| Template | File |
|----------|------|
| Basic | user-prompt-basic.ts |
| Planning | user-prompt-planning.ts |
| Professional | user-prompt-professional.ts |
| Context Basic | context-user-prompt-basic.ts |
| Context Planning | context-user-prompt-planning.ts |
| Context Professional | context-user-prompt-professional.ts |
