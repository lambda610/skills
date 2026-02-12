# DeepWiki Scan Workflow

Analyze codebase structure and generate overview documentation.

## When to Use

- Starting documentation for a new codebase
- Understanding project structure
- Identifying key components
- Technology stack detection

## Steps

### 1. Directory Analysis

1. List directory structure recursively (max depth 3-4)
2. Identify key directories (src/, tests/, docs/, config/)
3. Find entry points (main.ts, index.js, App.tsx)
4. Note build and config files

### 2. Technology Detection

Look for indicators:
- `package.json` / `requirements.txt` → Node.js / Python
- `tsconfig.json` → TypeScript
- `pyproject.toml` / `setup.py` → Python
- `go.mod` → Go
- `Cargo.toml` → Rust
- `pom.xml` / `build.gradle` → Java

### 3. File Inventory

List important files:
- Entry points
- Configuration files
- Main components
- Test files

### 4. Entry Points Discovery

Identify where the app starts:
- `src/main.ts` / `index.js` → Main entry
- `src/App.tsx` / `App.vue` → Root component
- `config/` → Configuration files

## Output Template

Create a comprehensive overview document:

```
# [Project Name] - Codebase Overview

## Quick Summary
Brief description of the project.

## Technology Stack
- **Language:** [TypeScript/Python/etc.]
- **Framework:** [React/Express/Django/etc.]
- **Build:** [Vite/Webpack/etc.]
- **Testing:** [Jest/Vitest/etc.]

## Directory Structure
[Tree structure]

## Key Components
| Component | Path | Purpose |
|-----------|------|---------|
| [Name] | src/[path] | [Description] |

## Entry Points
- **Main:** [File] - [Purpose]
- **Config:** [Files]

## Dependencies
- **Internal:** [Key modules]
- **External:** [Key packages]

## File Count
- Total: [N] files
- Code: [N] | Tests: [N] | Config: [N]

## Next Steps
- [ ] Generate detailed API docs
- [ ] Create module breakdown
- [ ] Document architecture
```

## Example

**Input:**
```
/deepwiki-scan ./my-project
```

**Output:**
```
# My Project - Codebase Overview

## Quick Summary
A React-based web application for task management.

## Technology Stack
- **Frontend:** React 18, TypeScript
- **Build:** Vite
- **Testing:** Vitest
- **Styling:** TailwindCSS

## Directory Structure
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

## Key Components
| Component | Path | Purpose |
|-----------|------|---------|
| App | src/App.tsx | Root component |
| API | src/api/client.ts | API client |

## Next Steps
- [ ] Generate detailed API docs
```

## Usage

```bash
/deepwiki-scan [path] --depth=[full|medium|shallow]
```

## Output Location

```
.deepwiki/scan/
├── overview.md
├── file-inventory.md
└── tech-stack.md
```
