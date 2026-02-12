# DeepWiki Generate Workflow

Generate comprehensive documentation for a codebase.

## When to Use

- Creating complete project documentation
- Preparing for AI context injection
- Documenting legacy codebases
- Onboarding new team members

## Steps

### 1. Architecture Documentation

Create architecture section with:
- System overview
- Component breakdown
- Data flow patterns
- Design decisions

### 2. API Documentation

Document all public APIs:
- Endpoints/functions
- Request/response formats
- Data types and interfaces
- Error handling

### 3. Module Breakdown

For each module:
- Purpose and responsibilities
- Files included
- Public exports
- Dependencies

### 4. File Documentation

For key files:
- Location and purpose
- Key functions/classes
- Related files

## Output Structure

Generate these files in `docs/deepwiki/`:

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

**Input:**
```
/deepwiki-generate --output=docs --depth=full
```

**Generated Structure:**
```
docs/deepwiki/
├── README.md
│   # Project: MyApp
│   # A React task manager
│   ## Quick Links
│   - [Architecture](ARCHITECTURE.md)
│   - [API Reference](API.md)
│   - [Modules](MODULES.md)
├── ARCHITECTURE.md
├── API.md
└── MODULES.md
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

1. Run `/deepwiki-scan` first for better results
2. Focus on public APIs — private details optional
3. Use code examples — explain with context
4. Link related modules — show relationships
5. Update iteratively — docs improve with use

## Output Location

Default: `docs/deepwiki/` directory
