# API Documentation Guide

This guide helps generate comprehensive API reference documentation.

## Overview

API documentation provides a complete reference of all public interfaces, functions, classes, and types.

## When to Use

- Creating library documentation
- Documenting web service APIs
- Generating SDK references
- Building developer portals

## Key Sections

### 1. Quick Index

| Category | Count |
|----------|-------|
| Functions | N |
| Classes | N |
| Types | N |
| Constants | N |

### 2. Functions

For each public function:

```typescript
function functionName(param1: Type, param2: Type): ReturnType
```

**Location:** `src/path/to/file.ts`

**Description:** What the function does

**Parameters:**
| Name | Type | Required | Description |
|------|------|----------|-------------|
| param1 | Type | Yes | Description |

**Returns:** What gets returned

**Example:**
```typescript
const result = functionName(value);
```

### 3. Classes

```typescript
class ClassName
```

**Location:** `src/path/to/file.ts`

**Constructor:**
```typescript
new ClassName(options: Options)
```

**Properties:**
| Property | Type | Description |
|----------|------|-------------|
| prop | Type | Description |

**Methods:**
| Method | Description |
|--------|-------------|
| method() | What it does |

### 4. Types & Interfaces

```typescript
// Enum or Union
type Status = 'pending' | 'done';

// Interface
interface Config {
  key: string;
  optional?: boolean;
}
```

### 5. API Endpoints (for web apps)

| Method | Path | Handler | Description |
|--------|------|---------|-------------|
| GET | /api/users | getUsers | List users |
| POST | /api/users | createUser | Create user |

**Request/Response formats**

### 6. Events

| Event | Payload | Description |
|-------|---------|-------------|
| click | { x, y } | User clicked |

### 7. Errors

| Code | Message | Cause |
|------|---------|-------|
| E001 | "Not found" | Resource doesn't exist |

## Output Location

```
docs/deepwiki/API.md
```

## Tips

- Start with exported (public) APIs
- Check `index.ts` barrel files
- Include working examples
- Document edge cases
- Note version compatibility

## See Also

- [ARCHITECTURE.md](./ARCHITECTURE.md) for system design
- [SCAN_GUIDE.md](./SCAN_GUIDE.md) for analysis methodology
