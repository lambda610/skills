---
name: deepwiki
description: "AI-powered local codebase documentation generator. Use for: (1) Scanning codebase structure, (2) Generating comprehensive documentation, (3) Creating API references and architecture diagrams, (4) Analyzing code organization and dependencies."
---

# DeepWiki — Local Codebase Documentation Generator

AI-powered local documentation generator for codebases. Generate comprehensive Markdown documentation from your codebase.

## Overview

DeepWiki analyzes your codebase and generates:
- **Architecture Overview** — System design and components
- **API Documentation** — Endpoints, interfaces, and contracts
- **Module Relationships** — Dependencies and data flow
- **Code Patterns** — Architectural decisions and patterns used

## Claude Code Usage

Simply describe what you need:

```bash
"Analyze this codebase structure"
"Generate documentation for this project"
"Document the API and modules"
"Scan the code and create architecture docs"
```

The skill will automatically trigger and help you generate comprehensive documentation.

## OpenClaw Usage

### Quick Scan
```
/deepwiki-scan [project-path]
```

### Full Documentation
```
/deepwiki-generate
```

### Specific Module
```
/deepwiki-module [module-path]
```

## For Detailed Guidance

See [SCAN_GUIDE.md](references/SCAN_GUIDE.md) for scan workflow details.
See [GENERATE_GUIDE.md](references/GENERATE_GUIDE.md) for generate workflow details.

## Workflows

### 1. Scan

Analyze codebase structure:
- Directory tree
- Key files identification
- Technology detection
- Entry points discovery

### 2. Generate

Create comprehensive docs:
- Architecture section
- API documentation
- Module breakdown
- Code relationships
- File inventory

### 3. Export

Output formats:
- Markdown files
- Structured JSON
- Documentation index

## Output Structure

```
docs/
├── README.md              # Project overview
├── ARCHITECTURE.md        # System design
├── API.md                 # API reference
├── MODULES.md             # Module breakdown
├── FILE_INVENTORY.md      # Complete file list
└── .deepwiki/            # Internal analysis
```

## Configuration

### Options

```yaml
deepwiki:
  scan:
    depth: "full"          # full, medium, shallow
    ignore:                 # patterns to skip
      - "**/node_modules/**"
      - "**/.git/**"
      - "**/dist/**"
  output:
    format: "markdown"     # markdown, json
    include:                # sections to include
      - architecture
      - api
      - modules
      - file-inventory
```

## Examples

### Basic

```bash
/deepwiki-generate --depth=full --output=docs
```

### Specific Focus

```bash
/deepwiki-generate --focus=api --output=api-docs.md
```

### Exclude Patterns

```bash
/deepwiki-scan --ignore="**/test/**,**/migrations/**"
```

## Best Practices

### For Large Codebases

1. **Start with scan** to get overview
2. **Generate module-by-module** for better results
3. **Use depth=shallow** for initial analysis

### For Small Projects

- Use `depth=full` for complete analysis
- Generate all sections

### For API-Focused Docs

```bash
/deepwiki-generate --focus=api --include=endpoints,interfaces
```

## Tips

- **Be specific** about what you want to document
- **Iterative approach** works best for large projects
- **Review generated docs** and add missing context
- **Use as a starting point** — refine as needed

## Integration

### With Claude Code

DeepWiki works great with Claude Code for:
- Context injection
- Code understanding
- Documentation updates

### With Git

Generate docs on:
- New releases
- Major PRs
- Project milestones

## Credits

Inspired by DeepWiki (deepwiki.com) and Devin by CognitionAI.
