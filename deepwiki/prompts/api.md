# API Documentation Prompt

Use this prompt to generate API reference documentation.

## Prompt Template

```
Analyze the codebase and generate comprehensive API documentation.

### Project Context
[Project name]: [Brief description]
Technology stack: [List technologies]

### Analysis Scope
Find and document:
1. Public functions and their signatures
2. Classes and their public methods
3. API endpoints (if web app)
4. Data types and interfaces
5. Event handlers and callbacks
6. Configuration options

### Output Format

```markdown
# [Project] API Reference

## Quick Index

| Category | Items |
|----------|-------|
| Functions | [N] |
| Classes | [N] |
| Types | [N] |
| Constants | [N] |

## Functions

### functionName

**Signature:**
```typescript
function functionName(param1: Type, param2: Type): ReturnType
```

**Location:** `src/path/to/file.ts`

**Description:**
[Brief description of what the function does]

**Parameters:**
| Name | Type | Description |
|------|------|-------------|
| param1 | Type | [Description] |
| param2 | Type | [Description] |

**Returns:** [What it returns]

**Example:**
```typescript
const result = functionName(value, options);
```

**Related:**
- [Other function]
```

## Classes

### ClassName

**Location:** `src/path/to/file.ts`

**Description:**
[Brief class description]

**Constructor:**
```typescript
new ClassName(options: Options)
```

**Properties:**
| Property | Type | Description |
|----------|------|-------------|
| prop | Type | [Description] |

**Methods:**
| Method | Description |
|--------|-------------|
| methodName() | [What it does] |

**Example:**
```typescript
const instance = new ClassName({ option: value });
instance.method();
```

## Types and Interfaces

```typescript
// Type: TypeName
type TypeName = 'value1' | 'value2';

// Interface: InterfaceName
interface InterfaceName {
  property: Type;
  optionalProp?: Type;
}
```

## Events

| Event | Handler | Description |
|-------|---------|-------------|
| eventName | (data: Data) => void | [Description] |

## Configuration

```typescript
interface Config {
  option1: Type;  // Description
  option2: Type;  // Description
}
```

## Error Reference

| Error Code | Message | Cause |
|------------|---------|-------|
| ERR_NAME | "Message" | [Why it happens] |
```

### Files to Analyze
[Glob patterns for API files]

### Ignore Patterns
[Patterns to skip - tests, internal helpers]
```

## Usage

```bash
/deepwiki-api [project-path]
```

## Tips

- Start with exported modules (public API)
- Look for index/barrel files
- Check type definitions (.d.ts files)
- Note any decorators or annotations
- Include usage examples where helpful
