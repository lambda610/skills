# DeepWiki Generate Guide

Use this guide when generating comprehensive, professional documentation.

## Philosophy

**Good documentation tells a story.** It explains not just what the code does, but why it does it and how to use it.

## Documentation Sections

### 1. Project Overview
The "电梯演讲" - can you explain this project in 2-3 sentences?

### 2. Architecture
High-level design, components, and how they interact

### 3. API Reference
Complete function/class signatures with descriptions

### 4. Module Guide
How to use and extend different parts

### 5. Data Reference
Types, schemas, and data contracts

### 6. Cookbook
Common tasks and how to accomplish them

## Detailed Templates

### Project Overview Template

```markdown
# [Project Name]

## One-Liner
[One sentence describing the project]

## Extended Description

### What It Does
[Brief explanation of core functionality]

### Why It Exists
[Problem it solves]

### Key Features
- [Feature 1]: [Brief description]
- [Feature 2]: [Brief description]
- [Feature 3]: [Brief description]

## Quick Start

### Installation
```bash
[Installation commands]
```

### Basic Usage
```[language]
[Minimal working example]
```

## Project Status
- 🟢 Active / 🔴 Archived / 🟡 Maintenance
- Last updated: [Date]
- [Additional status info]
```

### Architecture Template

```markdown
# Architecture

## High-Level Overview

```
[System diagram - ASCII or mermaid]
```

## Core Components

### [Component 1]

**Purpose:** [What problem it solves]

**Responsibilities:**
- [Responsibility 1]
- [Responsibility 2]

**Dependencies:**
- [Component 2] - [Relationship]
- [External Lib] - [Purpose]

**Located:** `src/path/component.ts`

### [Component 2]

**Purpose:** [What problem it solves]

...

## Data Flow

### [Flow Name]

```
[Step 1] → [Step 2] → [Step 3]
```

**Description:** [How this flow works]

## Architectural Decisions

| Decision | Context | Chosen Solution | Rationale |
|----------|---------|-----------------|-----------|
| [ADR-001] | [Problem] | [Solution] | [Why this over alternatives?] |

See [Architecture Decision Records](ADR.md) for details.

## Security

- [Security consideration 1]
- [Security consideration 2]

## Scalability

- [Scaling approach 1]
- [Scaling approach 2]
```

### API Reference Template

```markdown
# API Reference

## Getting Started

### Base URL
```
https://api.example.com/v1
```

### Authentication
All API requests require:
```http
Authorization: Bearer <token>
```

## Endpoints

### GET /resource

**Description:** Retrieves a list of resources.

**Parameters:**

| Name | Type | Required | Description |
|------|------|----------|-------------|
| limit | integer | No | Max items (default: 20) |
| offset | integer | No | Pagination offset |

**Response:**

```json
{
  "data": [...],
  "meta": {
    "total": 100,
    "limit": 20,
    "offset": 0
  }
}
```

**Errors:**

| Code | Meaning |
|------|---------|
| 400 | Invalid parameters |
| 401 | Unauthorized |
| 404 | Resource not found |

---

## Classes

### ClassName

**Location:** `src/path/file.ts:42`

**Purpose:** [What this class represents]

#### Constructor

```typescript
new ClassName(config: ConfigOptions)
```

#### Properties

| Property | Type | Description |
|----------|------|-------------|
| property | Type | What it holds |

#### Methods

##### methodName()

```typescript
async methodName(params: Params): Promise<Return>
```

**Purpose:** [What this method does]

**Parameters:**

| Param | Type | Description |
|-------|------|-------------|
| input | Type | [Description] |

**Returns:** [What's returned]

**Throws:**
- `ErrorType` - When [condition]

**Example:**
```typescript
[Usage example]
```

---

## Type Definitions

```typescript
// Domain types used throughout the API

interface DomainType {
  id: string;
  name: string;
  createdAt: Date;
}
```

### Module Template

```markdown
# [Module Name]

## Overview

**Purpose:** [What this module provides]

**Location:** `src/module/`

**Exports:**

| Export | Type | Description |
|--------|------|-------------|
| `exportName` | function | [Description] |

## Installation

```bash
[Installation if separate]
```

## Usage

### Basic Example

```typescript
import { exportName } from 'module';

const result = exportName({
  // Options
});
```

### Advanced Usage

```typescript
[More complex example]
```

## API

### `exportName(options)`

**Purpose:** [What it does]

**Parameters:**

| Param | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| option1 | string | Yes | - | [Description] |
| option2 | number | No | 10 | [Description] |

**Returns:** `ReturnType` - [What it returns]

**Example:**

```typescript
[Working example]
```

## Recipes

### How to: [Common Task 1]

```typescript
[Code example]
```

### How to: [Common Task 2]

```typescript
[Code example]
```

## Related
- [Related module 1]
- [Related module 2]
```

### Data Schema Template

```markdown
# Data Reference

## Overview

This document describes the data types, schemas, and contracts used in the project.

## Domain Types

### User

```typescript
interface User {
  /** Unique identifier */
  id: string;
  
  /** User's display name */
  name: string;
  
  /** Email address */
  email: string;
  
  /** ISO 8601 timestamp */
  createdAt: string;
  
  /** User's role */
  role: 'admin' | 'user' | 'guest';
}
```

### [Other Types]

```typescript
[Type definitions]
```

## Validation Rules

| Field | Rule | Error Message |
|-------|------|---------------|
| email | email() | Must be a valid email |
| password | min(8) | Must be at least 8 characters |

## Data Flow

```
[User Input] → [Validation] → [Transformation] → [Storage] → [Response]
```

## Migrations

### Version 1 → 2

Changes:
- Added `email` field
- Renamed `userName` → `name`
```

## Documentation Quality Checklist

- [ ] All public APIs documented
- [ ] Code examples included and tested
- [ ] Error conditions documented
- [ ] Type signatures accurate
- [ ] Cross-references added
- [ ] "Why" explained, not just "what"
- [ ] Common use cases covered
- [ ] Related resources linked

## Output Structure

```
docs/
├── README.md              # Project overview + quick start
├── ARCHITECTURE.md        # System design + components
├── API.md                 # Complete API reference
├── MODULES.md             # Module guides + recipes
├── DATA.md               # Data schemas + types
├── TUTORIAL.md           # Step-by-step guides
└── reference/
    ├── ADR.md            # Architecture decisions
    └── glossary.md       # Term definitions
```
