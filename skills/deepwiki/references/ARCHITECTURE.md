# Architecture Documentation Guide

This guide helps generate comprehensive architecture documentation for any codebase.

## Overview

Architecture documentation explains **how** the system works at a high level—not just what files exist, but why the system is designed that way.

## When to Use

- Onboarding new team members
- Planning refactoring or migrations
- Creating technical specs
- Reviewing architectural decisions

## Key Sections

### 1. System Overview

Brief description of what the system does and its primary goals.

### 2. High-Level Architecture

Visual representation of the system components and their relationships.

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Client    │────▶│   Server    │────▶│  Database   │
└─────────────┘     └─────────────┘     └─────────────┘
```

### 3. Core Components

| Component | Purpose | Dependencies |
|-----------|---------|--------------|
| Name | What it does | List |

### 4. Data Flow

How data moves through the system:
1. User action → API request
2. Server processes → Business logic
3. Database operations → Response

### 5. Architectural Decisions

| Decision | Rationale | Trade-offs |
|----------|-----------|------------|
| Choice | Why made | Costs/Benefits |

### 6. Design Patterns

| Pattern | Where Used | Purpose |
|---------|------------|---------|
| React Compound Component | BentoGrid | Flexible composition |

### 7. Infrastructure

- Deployment target
- External services
- CI/CD pipeline

## Output Location

```
docs/deepwiki/ARCHITECTURE.md
```

## See Also

- [SCAN_GUIDE.md](./SCAN_GUIDE.md) for analysis methodology
- [API.md](./API.md) for API documentation
