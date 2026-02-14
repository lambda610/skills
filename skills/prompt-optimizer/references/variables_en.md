# Variable Processing

Extract variables from prompts, or generate variable values based on context.

## Variable Extraction

### Function

Automatically identify and extract variable placeholders from prompts.

### Trigger

```
extract variables:
Please generate an article about {topic}, {word_count} words
```

### Output Format

```json
{
  "variables": [
    {
      "name": "topic",
      "description": "Article topic",
      "example": "AI",
      "required": true
    },
    {
      "name": "word_count",
      "description": "Word count requirement",
      "example": "1000",
      "required": true
    }
  ]
}
```

---

## Variable Value Generation

### Function

Suggest possible values for variables based on prompt context.

### Trigger

```
generate variable values:
template: {name} is a {profession} good at {skill}
context: tech industry, technical writing
```

### Output Format

```json
{
  "suggestions": [
    {
      "name": "name",
      "value": "John Smith",
      "reason": "Common English name"
    },
    {
      "name": "profession",
      "value": "Technical Writer",
      "reason": "Fits tech industry context"
    }
  ]
}
```

---

## Usage Examples

### Example 1: Variable Extraction

**Input**:
```
extract variables:
Please write an article about {product} in {type} for {audience}, approximately {word_count} words
```

**Output**:
```json
{
  "variables": [
    {
      "name": "product",
      "description": "Product name",
      "example": "Smartwatch",
      "required": true
    },
    {
      "name": "type",
      "description": "Article type",
      "example": "Review article",
      "required": true
    },
    {
      "name": "audience",
      "description": "Target audience",
      "example": "Tech enthusiasts",
      "required": true
    },
    {
      "name": "word_count",
      "description": "Word count",
      "example": "2000",
      "required": false
    }
  ]
}
```

---

## Trigger Keywords

| Function | Keywords |
|----------|----------|
| Variable Extraction | `extract variables:`, `variables:` |
| Variable Generation | `generate variables:`, `generate values:` |

---

## Corresponding Templates

| Function | Template |
|----------|----------|
| Variable Extraction | variableExtractionTemplate |
| Variable Generation | variableValueGenerationTemplate |
