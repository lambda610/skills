# DeepWiki Scan Workflow

Analyze codebase structure and generate overview documentation.

## When to Use

- Starting documentation for a new codebase
- Understanding project structure
- Identifying key components
- Technology stack detection

## Steps

### 1. Directory Analysis

```markdown
## Directory Structure

```
[project-root]/
├── src/                  # Source code
├── tests/                # Test files
├── docs/                 # Documentation
├── config/               # Configuration
└── [other dirs]
```

**Output:**
- Tree structure visualization
- Directory purposes
- Key entry points
```

### 2. Technology Detection

Identify technologies used:

```markdown
## Technology Stack

| Layer | Technology | Evidence |
|-------|------------|----------|
| Language | TypeScript | tsconfig.json |
| Framework | React | package.json, react |
| Build | Vite | vite.config.ts |
| Testing | Vitest | vitest.config.ts |
```

### 3. File Inventory

List all important files:

```markdown
## Key Files

| File | Purpose | Lines |
|------|---------|-------|
| src/main.ts | Entry point | 50 |
| src/App.tsx | Main component | 200 |
| src/api/client.ts | API client | 150 |
```

### 4. Entry Points Discovery

Identify where the app starts:

```markdown
## Entry Points

- **Main:** src/main.ts
- **Tests:** src/**/*.test.ts
- **Config:** vite.config.ts, tsconfig.json
```

## Output Template

```markdown
# [Project Name] - Codebase Overview

## Quick Summary

Brief description of the project.

## Technology Stack

- **Frontend:** [Tech]
- **Backend:** [Tech]
- **Database:** [Tech]
- **Build Tool:** [Tech]
- **Testing:** [Tech]

## Directory Structure

```
[Tree]
```

## Key Components

| Component | Path | Purpose |
|-----------|------|---------|
| [Name] | [Path] | [Description] |

## Entry Points

- [File]: [Purpose]
- [File]: [Purpose]

## Dependencies

- **Internal:** [List]
- **External:** [List]

## File Count

- Total files: [N]
- Code files: [N]
- Test files: [N]
- Config files: [N]

## Next Steps

- [ ] Generate detailed API docs
- [ ] Create module breakdown
- [ ] Document architecture
```

## Example

### Input

```
/deepwiki-scan ./my-project
```

### Output

```markdown
# My Project - Codebase Overview

## Quick Summary

A React-based web application for task management.

## Technology Stack

- **Frontend:** React 18, TypeScript
- **Build:** Vite
- **Testing:** Vitest
- **Styling:** TailwindCSS

## Directory Structure

```
my-project/
├── src/
│   ├── components/
│   ├── hooks/
│   ├── utils/
│   ├── App.tsx
│   └── main.tsx
├── tests/
├── config/
└── package.json
```

...

## Next Steps

- [ ] Generate detailed API docs
- [ ] Create module breakdown
```

## Usage

```bash
/deepwiki-scan [path] --depth=[full|medium|shallow] --ignore=[patterns]
```

## Output Location

```
.deepwiki/scan/
├── overview.md
├── file-inventory.md
└── tech-stack.md
```
