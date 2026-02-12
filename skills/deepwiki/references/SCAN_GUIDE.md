# DeepWiki Scan Guide

Use this guide when performing deep code analysis and scanning a codebase for documentation.

## Overview

This guide extends basic scanning with **deep code analysis** capabilities. The goal is to understand not just what files exist, but what the code actually does, how it works, and why it was designed that way.

## Core Principles

### 1. Read Code Content, Not Just File Names

Don't just list files—read and understand them. For each key file:

- Read the actual source code
- Identify business logic and workflows
- Extract function signatures and contracts
- Find design patterns and architectural decisions
- Map data flow and state management

### 2. Ask "What" and "Why"

For every component, ask:
- **What** does this code do?
- **Why** was it designed this way?
- **How** does it interact with other parts?
- **When** is it used?

### 3. Look Beyond Structure

Find:
- Implicit dependencies
- Event flows and callbacks
- State mutations
- Error handling patterns
- Configuration mechanisms

## Deep Scan Workflow

### Phase 1: Structure Analysis (Quick Scan)

```bash
# Get directory tree (limit depth for overview)
find . -type d -maxdepth 3 | head -100

# Find all source files by extension
find . -type f \( -name "*.ts" -o -name "*.js" -o -name "*.py" -o -name "*.go" \) | grep -v node_modules | grep -v ".git"

# List configuration files
find . -maxdepth 2 -type f \( -name "package.json" -o -name "tsconfig.json" -o -name "pyproject.toml" -o -name "go.mod" -o -name "Cargo.toml" \)
```

### Phase 2: Technology Detection

Analyze config files to understand the stack:

```bash
# Read package.json for Node projects
cat package.json | jq '{name, version, dependencies, devDependencies, scripts}'

# Read pyproject.toml for Python
cat pyproject.toml

# Read go.mod for Go projects
cat go.mod

# Check for framework indicators
find . -type f -name "*.config.*" -o -name "vue.config.*" -o -name "next.config.*" -o -name "astro.config.*"
```

### Phase 3: Entry Points Discovery

Find where execution starts:

```bash
# Main entry points
find . -type f \( -name "main.ts" -o -name "main.js" -o -name "index.ts" -o -name "index.js" -o -name "app.ts" -o -name "app.py" \) | grep -v node_modules

# Configuration entry points
find . -type f \( -name "config.*" -o -name "settings.*" \) | head -20

# Route/endpoint definitions
find . -type f \( -name "routes.*" -o -name "router.*" -o -name "*route*" \) | grep -v node_modules
```

### Phase 4: Deep Code Analysis (The Key Difference)

This is where we go beyond basic listing. **Read actual code content.**

#### Step 4a: Read Key Files in Detail

For the most important files, read the full content:

```bash
# Read entry point
cat src/main.ts

# Read root component (React/Vue)
cat src/App.tsx

# Read API/routing setup
cat src/router/index.ts

# Read core service files
cat src/services/*.ts

# Read utility files with business logic
cat src/utils/*.ts
```

#### Step 4b: Identify Business Logic

When reading code, look for:

```
1. WORKFLOW PATTERNS
   - Multi-step processes
   - User action handlers
   - Data transformation pipelines
   - Async operations and callbacks

2. DATA FLOW
   - Where data enters the system
   - How data is processed
   - Where data is stored
   - How data is returned to users

3. STATE MANAGEMENT
   - Global state stores
   - Context/providers
   - Mutable vs immutable patterns
   - State persistence

4. ERROR HANDLING
   - Try-catch patterns
   - Error boundaries
   - Fallback mechanisms
   - User feedback patterns
```

#### Step 4c: Extract API Signatures

For each public function/method, identify:

```typescript
// Read function signatures
export function processPayment(amount: number, currency: string): Promise<PaymentResult>

// Extract:
// - Function name: processPayment
// - Parameters: amount (number), currency (string)
// - Return type: Promise<PaymentResult>
// - Async: Yes
// - Export level: Public/external
```

#### Step 4d: Map Dependencies

Trace what each module depends on:

```bash
# Find imports in key files
grep -h "^import" src/*.ts src/**/*.ts 2>/dev/null | sort | uniq

# Find export statements
grep -h "^export" src/*.ts src/**/*.ts 2>/dev/null | sort | uniq

# Find class/interface definitions
grep -h "^interface\|^type\|^class" src/*.ts src/**/*.ts 2>/dev/null | sort | uniq
```

### Phase 5: Pattern Recognition

Identify recurring patterns in the code:

```
ARCHITECTURAL PATTERNS:
- [ ] MVC / MVP / MVVM
- [ ] Repository pattern
- [ ] Service layer
- [ ] Dependency injection
- [ ] Factory pattern
- [ ] Singleton usage
- [ ] Observer/Pub-Sub
- [ ] Middleware pipeline

CODE ORGANIZATION:
- [ ] Feature-based vs layer-based
- [ ] Domain-driven design
- [ ] Component composition
- [ ] Hook-based logic reuse

STATE PATTERNS:
- [ ] Centralized store (Redux, Vuex)
- [ ] Context API
- [ ] Local state
- [ ] URL/state synchronization
```

## Deep Analysis Prompts

Use these prompts to guide deep analysis:

### Prompt 1: Business Logic Discovery

```
Read through the main source files and identify:

1. WHAT BUSINESS PROBLEMS does this code solve?
   - List the core features/workflows
   - Describe each in 1-2 sentences

2. WHO are the users and what can they do?
   - User roles or personas
   - Actions available to each

3. WHAT DATA does the system manage?
   - Core entities (User, Product, Order, etc.)
   - Relationships between entities

4. HOW do workflows execute?
   - Step-by-step for main user journeys
   - Include async operations and API calls

5. WHERE does data come from and go?
   - External APIs integrated
   - Database/storage systems
   - Third-party services
```

### Prompt 2: Architecture Deep Dive

```
Analyze the code architecture by tracing:

1. ENTRY POINTS
   - Where does execution start?
   - What initializes the app?
   - How are routes/endpoints registered?

2. COMPONENT HIERARCHY
   - Parent-child relationships
   - Data passing patterns
   - Communication methods (props, events, context, callbacks)

3. LAYER BOUNDARIES
   - Presentation layer components
   - Business logic layer
   - Data access layer
   - Infrastructure/external integration

4. DEPENDENCY FLOW
   - What does Component A need from Component B?
   - How are dependencies injected?
   - What's the coupling level?

5. EXTENSION POINTS
   - Where can behavior be customized?
   - Plugin systems
   - Hook/callback opportunities
   - Configuration options
```

### Prompt 3: Data Flow Mapping

```
Map the data flow through the system:

1. DATA ENTRY POINTS
   - User inputs (forms, API calls, file uploads)
   - System events (timers, webhooks)
   - External data sources

2. DATA TRANSFORMATIONS
   - Raw data → processed data
   - Validation steps
   - Formatting/conversion
   - Aggregation/computation

3. DATA STORAGE
   - Where is data persisted?
   - In-memory caches
   - LocalStorage/cookies
   - Database operations

4. DATA OUTPUTS
   - UI rendering
   - API responses
   - File exports
   - External system calls

5. STATE CHANGES
   - What triggers state updates?
   - Optimistic updates?
   - Rollback mechanisms?
```

### Prompt 4: API Signature Extraction

```
For all public APIs, extract:

1. FUNCTION SIGNATURES
   name, parameters (with types), return type, async/sync

2. CLASS CONSTRUCTORS
   parameters, initialization logic

3. INTERFACE/TYPE DEFINITIONS
   all properties and their types

4. ERROR TYPES
   custom error classes or error codes

5. EVENT SIGNATURES
   event names, payload structures

6. CONFIGURATION
   config object structure, environment variables
```

### Prompt 5: Design Decision Extraction

```
Identify design decisions made in the codebase:

1. ARCHITECTURAL DECISIONS
   - Why was this structure chosen?
   - What alternatives were considered?
   - What trade-offs were made?

2. TECHNOLOGY CHOICES
   - Why this framework over others?
   - Why this library for X feature?
   - Any custom solutions vs off-the-shelf?

3. PATTERN SELECTIONS
   - Why this pattern for this problem?
   - How does it affect testability?
   - How does it affect maintainability?

4. CONVENTION CHOICES
   - Naming conventions
   - File organization
   - Code style preferences

5. PERFORMANCE DECISIONS
   - Caching strategies
   - Lazy loading decisions
   - Bundle/performance optimizations
```

## Output Template for Deep Scan

```markdown
# [Project] - Deep Code Analysis

## Executive Summary
[Brief 2-3 sentence description of what this project does and its core value]

## Technology Stack
| Category | Technology | Version/Purpose |
|----------|------------|-----------------|
| Language | [TypeScript/Python/etc.] | [Version if applicable] |
| Framework | [React/Django/Express/etc.] | [Version] |
| Build Tool | [Vite/Webpack/etc.] | - |
| Testing | [Jest/Vitest/etc.] | - |
| [Other] | [Lib] | [Purpose] |

## Architecture Overview

### High-Level Design
[Describe the overall architecture pattern - e.g., microservices, monolith, serverless, etc.]

### Core Layers
| Layer | Responsibility | Key Components |
|-------|---------------|-----------------|
| Presentation | [What it handles] | [Components] |
| Business Logic | [What it handles] | [Services/Controllers] |
| Data Access | [What it handles] | [Repositories/DAOs] |
| Infrastructure | [What it handles] | [Config/Middleware] |

### Key Entry Points
| Entry Point | File | Purpose |
|-------------|------|---------|
| App Start | `src/main.ts` | Initializes app |
| Routes | `src/router/index.ts` | Defines all routes |
| [Other] | [File] | [Purpose] |

## Business Logic

### Core Features
| Feature | Location | Description |
|---------|----------|-------------|
| [Feature 1] | `src/features/x/` | [What it does] |
| [Feature 2] | `src/features/y/` | [What it does] |

### User Workflows
#### Workflow 1: [Name]
```
User Action → [Handler] → [Service] → [Data Layer] → [Response]
```
Steps:
1. [Step]
2. [Step]
3. [Step]

#### Workflow 2: [Name]
```
[Flow description]
```

### Data Entities
| Entity | Properties | Relationships |
|--------|------------|---------------|
| User | id, name, email, password | 1:N with Order |
| Order | id, userId, items, total | N:1 with User |

## API Reference

### Public Functions
| Function | Signature | Purpose |
|----------|-----------|---------|
| `processPayment` | `(amount, currency) => Promise<PaymentResult>` | [Description] |
| `createUser` | `(data) => Promise<User>` | [Description] |

### Classes
| Class | Purpose | Key Methods |
|-------|---------|-------------|
| `AuthService` | Authentication logic | login, logout, register |
| `DataFetcher` | HTTP requests | get, post, put, delete |

### Types/Interfaces
```typescript
interface User {
  id: string;
  name: string;
  email: string;
}
```

## Design Patterns Used

| Pattern | Location | Purpose |
|---------|----------|---------|
| Repository | `src/repos/` | Data access abstraction |
| Service Layer | `src/services/` | Business logic |
| Observer | `src/events/` | Event handling |
| Factory | `src/factories/` | Object creation |

## Dependencies

### Internal Dependencies
```
[Component A] → [Component B] (uses for auth)
[Component C] → [Component D] (depends on data)
```

### External Dependencies
| Package | Version | Purpose |
|---------|---------|---------|
| react | ^18.2.0 | UI framework |
| axios | ^1.6.0 | HTTP client |

### Dependency Graph (Simplified)
```
src/
├── components/  → depends on → hooks/, utils/
├── hooks/        → depends on → utils/, api/
├── api/          → depends on → config/, types/
└── utils/        → [no external deps]
```

## Data Flow

### Example Flow: [Name]
```
[User Input] → [Component] → [Service] → [API] → [Database]
              ← [Response] ← [Data] ← [Result]
```

### State Management
| State | Location | Type | Purpose |
|-------|----------|------|---------|
| User | `src/context/Auth.tsx` | Context | Current user session |
| Cart | `src/store/cart.ts` | Redux | Shopping cart items |

## Design Decisions

| Decision | Rationale | Trade-off |
|----------|-----------|-----------|
| Chose Redux for state | Need predictability | More boilerplate |
| Server-side rendering | SEO requirements | Higher complexity |

## Code Patterns

### Common Patterns
1. **Custom hooks** for reusable logic (`useAuth`, `useFetch`)
2. **Higher-order components** for cross-cutting concerns
3. **Repository pattern** for data access abstraction
4. **Middleware pipeline** for request processing

### Naming Conventions
- Components: PascalCase
- Hooks: camelCase starting with "use"
- Utils: camelCase
- Files: kebab-case

## File Inventory Summary
| Category | Count | Examples |
|----------|-------|----------|
| Components | 45 | `Button.tsx`, `Modal.tsx` |
| Services | 12 | `auth.ts`, `payment.ts` |
| Utils | 20 | `format.ts`, `validate.ts` |
| Types | 8 | `user.ts`, `api.ts` |

## Next Steps for Documentation
- [ ] Generate detailed API documentation
- [ ] Create architecture diagrams
- [ ] Document each feature module
- [ ] Add usage examples
```

## Tips for Deep Analysis

1. **Start Small, Expand Out**
   - Begin with entry points
   - Follow execution flow outward
   - Don't try to understand everything at once

2. **Read the Tests**
   - Tests reveal expected behavior
   - Show edge cases and error handling
   - Demonstrate how APIs should be used

3. **Check Configuration**
   - Environment variables reveal integrations
   - Config files show customization points
   - Build configs reveal optimization choices

4. **Look for Documentation Comments**
   - Often contain design rationale
   - May explain complex logic
   - Sometimes include usage examples

5. **Trace Data, Not Just Control Flow**
   - Data shows the "what"
   - Control flow shows the "how"
   - Both are needed for understanding

6. **Identify Domain Concepts**
   - Domain language appears in naming
   - Core entities often have dedicated modules
   - Business rules are in the logic, not UI

## Anti-Patterns to Watch For

- ❌ Just listing files without reading content
- ❌ Ignoring error handling and edge cases
- ❌ Missing async/await and callback chains
- ❌ Overlooking configuration and environment
- ❌ Forgetting about third-party integrations
