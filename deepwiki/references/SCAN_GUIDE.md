# DeepWiki Scan Guide

Use this guide when scanning a codebase for documentation.

## Quick Start

When asked to scan or analyze a codebase:

1. **Explore structure** - List files recursively
2. **Identify key files** - package.json, README.md, config files
3. **Detect technology** - Languages, frameworks, tools
4. **Find entry points** - main.ts, index.js, App.tsx

## Scan Workflow

### Step 1: Directory Exploration

```bash
# Get overview
ls -la
find . -type f -name "*.json" -o -name "*.md" | head -20

# Get tree structure (limit depth)
find . -type d -maxdepth 3 | head -50
```

### Step 2: Key Files Analysis

Check these files for context:
- `package.json` / `pyproject.toml` - Dependencies
- `README.md` - Project description
- `tsconfig.json` / `pyproject.toml` - Config
- `.gitignore` - Ignored patterns (reveals structure)

### Step 3: Technology Detection

Look for:
- `.ts`, `.tsx` → TypeScript
- `.py` → Python
- `.java` → Java
- `package.json` → Node.js
- `requirements.txt` → Python
- `go.mod` → Go
- `Cargo.toml` → Rust

### Step 4: Entry Points

Find where the app starts:
- `src/main.ts`, `src/index.ts`
- `app.js`, `index.js`
- `main.py`, `app.py`

## Output Template

```markdown
# [Project] - Codebase Overview

## Quick Summary
[Brief description from README or package.json]

## Technology Stack
- **Language:** [TypeScript/Python/etc.]
- **Framework:** [React/Express/Django/etc.]
- **Build:** [Vite/Webpack/etc.]
- **Testing:** [Jest/Vitest/etc.]

## Directory Structure
```
[Tree - use find command]
```

## Key Components
| Component | Purpose | Location |
|-----------|---------|----------|
| [Name] | [What it does] | src/[path] |

## Entry Points
- **Main:** [File]
- **Config:** [Files]

## Dependencies
- **Internal:** [Key modules]
- **External:** [Key packages]

## Next Steps
- [ ] Generate detailed API docs
- [ ] Document architecture
- [ ] Create module breakdown
```

## Tips

- Use tables for structured data
- Focus on structure, not implementation
- Identify patterns, don't list every file
- Note relationships between components
