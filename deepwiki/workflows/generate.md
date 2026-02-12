# DeepWiki Generate Workflow

Generate comprehensive documentation for a codebase.

## When to Use

- Creating complete project documentation
- Preparing for AI context injection
- Documenting legacy codebases
- Onboarding new team members

## Steps

### 1. Architecture Documentation

```markdown
# [Project] Architecture

## System Overview

Brief description of the system and its purpose.

## High-Level Architecture

```
[Architecture Diagram]
```

## Components

| Component | Responsibility | Dependencies |
|-----------|---------------|--------------|
| [Name] | [What it does] | [Depends on] |
```

### 2. API Documentation

```markdown
# [Project] API Reference

## Endpoints

| Method | Path | Description | Request | Response |
|--------|------|------------|---------|----------|
| GET | /api/users | List users | - | [User[]] |
| POST | /api/users | Create user | UserCreate | User |

## Data Types

```typescript
interface User {
  id: string;
  name: string;
  email: string;
}
```

## Error Codes

| Code | Meaning |
|------|---------|
| 400 | Bad Request |
| 401 | Unauthorized |
| 404 | Not Found |
```

### 3. Module Breakdown

```markdown
# Modules

## Module: [Name]

### Purpose
[What the module does]

### Files

| File | Purpose |
|------|---------|
| [File] | [Description] |

### Exports

```typescript
export { Function } from './file';
export class Class { ... }
```

### Dependencies
- [Module A]
- [Module B]
```

### 4. File Documentation

For each important file:

```markdown
## [filename.ext]

**Path:** `src/path/to/file.ext`

**Purpose:** [What this file does]

**Key Functions/Classes:**

| Name | Type | Description |
|------|------|-------------|
| [Name] | function | [Description] |

**Related Files:**
- [Related] - [Why related]
```

## Output Structure

```
docs/deepwiki/
├── README.md              # Overview + Quick Links
├── ARCHITECTURE.md        # System design
├── API.md                 # API reference
├── MODULES.md             # Module breakdown
├── FILE_INVENTORY.md      # All files listed
├── DEPENDENCIES.md        # Dependency graph
└── .deepwiki/
    ├── analysis.json      # Raw analysis
    └── structure.json     # Structure data
```

## Example

### Input

```
/deepwiki-generate --output=docs --depth=full
```

### Generated Structure

```
docs/deepwiki/
├── README.md
│   # Project: MyApp
│   # A React task manager
│   
│   ## Quick Links
│   - [Architecture](ARCHITECTURE.md)
│   - [API Reference](API.md)
│   - [Modules](MODULES.md)
│
├── ARCHITECTURE.md
│   # High-level design
│   # Components and interactions
│
├── API.md
│   # All endpoints
│   # Data types
│
└── MODULES.md
    # All modules documented
```

## Configuration Options

```yaml
generate:
  include:
    - architecture    # System design
    - api            # API reference
    - modules        # Module breakdown
    - file-inventory # Complete list
    - dependencies   # Dependency graph
  
  exclude:
    - "**/test/**"
    - "**/*.test.ts"
    - "**/node_modules/**"
```

## Quality Checklist

- [ ] Architecture makes sense
- [ ] All modules documented
- [ ] API complete and accurate
- [ ] File inventory up to date
- [ ] Cross-references work
- [ ] Examples provided

## Usage

```bash
/deepwiki-generate [path] --output=[dir] --include=[sections]
```

## Tips

1. **Run `/deepwiki-scan` first** for better results
2. **Focus on public APIs** — private details optional
3. **Use code examples** — explain with context
4. **Link related modules** — show relationships
5. **Update iteratively** — docs improve with use

## Output Location

Default: `docs/deepwiki/` directory
Custom: Specify with `--output`
