# DeepWiki Scan Guide

Use this guide when performing deep code analysis and documentation generation for a codebase.

## Core Principle: Deep Analysis, Not Just Listing

**Critical:** Do not just list files. Actually READ and UNDERSTAND the code content. The goal is to extract meaningful insights about architecture, business logic, and design decisions.

---

## Scan Workflow

### Phase 1: Structure Exploration (Quick Overview)

```bash
# Get directory tree with reasonable depth
find . -type d -maxdepth 3 | head -100

# Find key configuration and entry point files
find . -maxdepth 2 -type f \( -name "package.json" -o -name "pyproject.toml" -o -name "go.mod" -o -name "Cargo.toml" -o -name "*.config.*" -o -name "README.md" -o -name "index.ts" -o -name "main.py" -o -name "app.js" \)

# Get file type distribution
find . -type f \( -name "*.ts" -o -name "*.js" -o -name "*.py" -o -name "*.java" \) | wc -l
```

### Phase 2: Deep Content Analysis (THE IMPORTANT PART)

For each significant module/component, you MUST:

1. **Read actual source files** - Don't skip implementation details
2. **Identify business logic** - What problem does this solve?
3. **Extract function signatures** - Document actual APIs with parameters
4. **Map data flow** - How does data move through the system?
5. **Find design patterns** - What architectural patterns are used?

#### Deep Code Analysis Prompts

When analyzing any source file, ask yourself:

```
- What is the PRIMARY PURPOSE of this code?
- What BUSINESS LOGIC does it implement?
- What are the MAIN FUNCTIONS/CLASSES and what do they do?
- What DATA STRUCTURES are used?
- What EXTERNAL DEPENDENCIES does it have?
- What DESIGN PATTERNS are evident?
- How does data FLOW INTO and FLOW OUT of this component?
- What ERROR HANDLING/VALIDATION exists?
- What are the KEY DECISIONS made in this code?
```

### Phase 3: Architecture Discovery

```bash
# Find all entry points and main modules
find . -type f -name "*.ts" -o -name "*.js" -o -name "*.py" | xargs grep -l "export.*main\|export.*App\|export.*create\|@Component\|@Controller" 2>/dev/null | head -20

# Find configuration and environment setup
find . -maxdepth 2 -type f \( -name ".env*" -o -name "config*" -o -name "settings*" \)

# Find database models/schema definitions
find . -type f \( -name "*model*" -o -name "*schema*" -o -name "*entity*" -o -name "*migration*" \) | head -30

# Find API/routes definitions
find . -type f \( -name "*route*" -o -name "*controller*" -o -name "*endpoint*" -o -name "*handler*" \) | head -30
```

### Phase 4: Dependency Mapping

```bash
# Analyze imports to understand module relationships
for f in $(find . -type f -name "*.ts" -o -name "*.js" | head -50); do
  echo "=== $f ==="
  head -50 "$f" | grep -E "^import|^export" | head -20
done

# Build dependency graph mentally - note:
# - What modules import from what
# - What are the core utilities/helpers
# - What are the external packages heavily used
# - What are the circular dependencies
```

---

## Deep Analysis Checklist

Use this checklist to ensure thorough analysis:

### Technology Stack
- [ ] Primary language(s) identified
- [ ] Framework(s) detected
- [ ] Build tools and bundlers identified
- [ ] Testing framework(s) found
- [ ] Database and ORM identified
- [ ] External services/APIs used

### Architecture Components
- [ ] Entry points identified
- [ ] Main modules/packages identified
- [ ] Core business logic files located
- [ ] Configuration and environment handling found
- [ ] Data layer (models, schemas) identified
- [ ] API layer (routes, controllers) identified
- [ ] Service layer identified
- [ ] Utility/helper modules found

### Code Understanding
- [ ] Actually read top 10-20 most important files
- [ ] Understood main data structures
- [ ] Identified key function signatures
- [ ] Understood data flow between components
- [ ] Found design patterns used
- [ ] Identified error handling strategies
- [ ] Understood configuration management

### Business Logic
- [ ] Understood what the application DOES
- [ ] Identified main workflows/user journeys
- [ ] Found business rules and validation
- [ ] Understood data models and relationships
- [ ] Identified key algorithms or processing

---

## Output Template: Deep Scan Report

```markdown
# [Project Name] - Deep Code Analysis Report

## Executive Summary
[2-3 sentences describing what this project does and its main purpose]

## Technology Stack
| Category | Technology | Version/Notes |
|----------|------------|---------------|
| Language | [TypeScript/Python/etc] | [Version if known] |
| Framework | [React/Django/Express/etc] | [Version] |
| Database | [PostgreSQL/MongoDB/etc] | [If applicable] |
| Build Tool | [Vite/Webpack/etc] | |
| Testing | [Jest/Vitest/etc] | |
| Other Key | [Docker/Kubernetes/etc] | |

## Architecture Overview

### High-Level Design
[Describe the architectural pattern: MVC, layered, microservices, monolithic, serverless, etc.]

### System Boundaries
- **Input:** [User interfaces, APIs, cron jobs, webhooks, etc.]
- **Processing:** [What the system computes/processes]
- **Output:** [APIs, database writes, files, notifications, etc.]

### Core Components

| Component | Location | Purpose | Key Responsibilities |
|-----------|----------|---------|---------------------|
| [Name] | `src/path` | [One-line purpose] | [2-4 key responsibilities] |

## Data Flow Architecture

### Data Flow Diagram (Text-based)
```
[User/API] --> [Entry Point] --> [Router/Controller] --> [Service Layer] 
    --> [Data Access] --> [Database/External Service]
                          ^                       |
                          |_______________________|
                          [Response/Notification]
```

### Key Data Flows
1. **[Flow Name]:** [Description of how data moves]
2. **[Flow Name]:** [Description]

## Module Dependency Map

```
[Core Modules]
├── module-a/
│   ├── sub-module-a1  --> depends on --> module-b/utils
│   └── sub-module-a2
├── module-b/
│   ├── utils/         <-- core dependency --
│   └── services/      --> calls external APIs
└── module-c/
```

## Business Logic Summary

### Main Features/Services
1. **[Feature 1]:** [What it does]
2. **[Feature 2]:** [What it does]

### Key Business Rules
- [Rule 1]: [Where implemented and what it does]
- [Rule 2]: [Where implemented and what it does]

### Critical Workflows
1. **[Workflow Name]:**
   - **Trigger:** [What starts this workflow]
   - **Steps:** [Brief step-by-step]
   - **End State:** [What happens at the end]

## API Reference Preview

### Public Endpoints/Functions

| Endpoint/Function | Input | Output | Purpose |
|-------------------|-------|--------|---------|
| `POST /api/users` | User data | User object | Create new user |
| `UserService.create()` | UserData | Promise<User> | Business logic for user creation |

## Design Patterns & Decisions

### Architectural Patterns Identified
- **[Pattern Name]:** [Where used and why beneficial]
- **[Pattern Name]:** [Where used and why beneficial]

### Key Design Decisions
- **[Decision]:** [Context, choice made, and rationale]

### Code Conventions
- [Convention 1]: [What the codebase follows]
- [Convention 2]: [What the codebase follows]

## Dependencies Analysis

### External Packages (Key Ones)
| Package | Purpose | Usage Location |
|---------|---------|----------------|
| `express` | Web framework | All route handlers |
| `axios` | HTTP client | External API calls |

### Internal Dependencies
- **module-a** depends on: `module-b`, `module-c/utils`
- **module-b** depends on: `module-c/utils`, `database`

## Security & Validation

### Authentication/Authorization
- [How auth is handled]
- [Where implemented]

### Input Validation
- [Validation library/approach]
- [Where validation occurs]

## File Inventory Summary
- **Total source files:** [N]
- **Total lines of code:** [Approximate]
- **Largest modules:** [Top 3 by file count/size]

## Recommendations for Documentation
- [ ] Generate detailed API documentation
- [ ] Create sequence diagrams for key workflows
- [ ] Document configuration options
- [ ] Add code examples for main use cases
```

---

## Tips for Deep Analysis

1. **Read actual code, don't assume** - The only way to understand business logic is to read the implementation
2. **Follow the data** - Trace how data moves through the system
3. **Look for patterns** - Identify recurring structures and conventions
4. **Find the "why"** - Don't just list what exists, understand why it was designed that way
5. **Document decisions** - Note architectural choices and their rationale
6. **Connect the dots** - Show relationships between components
7. **Be specific** - Use actual function signatures, class names, and file paths
8. **Extract examples** - Find and document real usage examples
