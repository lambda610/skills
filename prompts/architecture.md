# Architecture Analysis Prompt

Use this prompt to generate architecture documentation.

## Prompt Template

```
Analyze the codebase structure and generate architecture documentation.

### Project Context
[Project name]: [Brief description]
Technology stack: [List technologies]

### Analysis Scope
Focus on:
1. System design principles
2. Component interactions
3. Data flow patterns
4. Architectural decisions
5. Design patterns used

### Output Format

```markdown
# [Project] Architecture

## Overview
[Brief system description]

## High-Level Architecture

```
[Architecture Diagram - ASCII or description]
```

## Core Components

| Component | Purpose | Dependencies |
|-----------|---------|--------------|
| [Name] | [What it does] | [List] |

## Data Flow

### [Flow 1]
```
[Step 1] → [Step 2] → [Step 3]
```

### [Flow 2]
```
[Step 1] → [Step 2]
```

## Architectural Decisions

| Decision | Rationale | Trade-offs |
|----------|-----------|------------|
| [Choice] | [Why] | [Cost] |

## Design Patterns

| Pattern | Where Used | Purpose |
|---------|------------|---------|
| [Pattern] | [Location] | [What it solves] |

## Scaling Considerations
- [Point 1]
- [Point 2]

## Potential Improvements
- [Idea 1]
- [Idea 2]
```

### Files to Analyze
[Glob patterns for key files]

### Ignore Patterns
[Patterns to skip]
```

## Usage

```bash
/deepwiki-architecture [project-path]
```

## Tips

- Start with entry points to understand flow
- Look for configuration files (often reveal architecture)
- Identify main domains/features
- Trace data through the system
- Note any external integrations
