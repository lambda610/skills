# DeepWiki Generate Guide

Use this guide when generating comprehensive documentation for a codebase.

## Generate Workflow

### Step 1: Full Scan

First, understand the complete codebase:
- List all source files
- Identify main modules
- Find public APIs
- Map dependencies

### Step 2: Analyze Each Section

#### Architecture Overview
- System design principles
- Component responsibilities
- Data flow patterns
- Design decisions made

#### API Reference
- Public functions and signatures
- Classes and methods
- Data types and interfaces
- Error handling

#### Module Breakdown
- Each module's purpose
- Files included
- Exports and public API
- Dependencies

#### Code Patterns
- Architectural patterns used
- Common conventions
- Design patterns

### Step 3: Generate Documentation Files

Create these files in `docs/` directory:

1. `README.md` - Project overview
2. `ARCHITECTURE.md` - System design
3. `API.md` - API reference
4. `MODULES.md` - Module breakdown
5. `FILE_INVENTORY.md` - Complete list

## Documentation Templates

### Architecture Section

```markdown
## Architecture

### High-Level Design
[Brief system description]

### Components
| Component | Responsibility | Dependencies |
|-----------|---------------|--------------|
| [Name] | [What it does] | [Depends on] |

### Data Flow
[How data moves through the system]
```

### API Section

```markdown
## API Reference

### Functions

#### functionName

**Signature:**
```typescript
function functionName(param: Type): ReturnType
```

**Location:** `src/path/file.ts`

**Description:**
[Brief description]

**Parameters:**
| Name | Type | Description |
|------|------|-------------|
| param | Type | [Description] |

**Returns:** [What it returns]
```

### Modules Section

```markdown
## Modules

### Module: [Name]

**Purpose:** [What the module does]

**Files:**
| File | Purpose |
|------|---------|
| [File] | [Description] |

**Exports:**
```typescript
export { Function } from './file';
```

**Dependencies:** [Related modules]
```

## Best Practices

- Use tables for structured data
- Include code examples
- Link related components
- Focus on public APIs
- Be consistent with formatting
- Don't document private internals

## Output Summary

When done, provide a summary:

```markdown
## Documentation Generated

- [x] README.md - Project overview
- [x] ARCHITECTURE.md - System design
- [x] API.md - API reference
- [x] MODULES.md - Module breakdown
- [x] FILE_INVENTORY.md - Complete file list

Total files: [N]
Lines of documentation: [N]
```
