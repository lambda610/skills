# DeepWiki Generate Guide

Use this guide when generating comprehensive documentation for a codebase. Focus on creating detailed, useful documentation that goes beyond surface-level file listings.

## Generate Workflow

### Phase 1: Comprehensive Scan

Before generating docs, perform thorough analysis:

1. **List and categorize all source files** by module/purpose
2. **Read key implementation files** - not just interfaces
3. **Map all dependencies** - internal and external
4. **Identify all public APIs** - functions, classes, endpoints
5. **Understand business workflows** - what and why, not just how

### Phase 2: Deep Analysis by Section

For each documentation section, you MUST:

- **Actually read the code** - Extract real signatures, not pseudo-code
- **Understand the purpose** - Document what and why, not just where
- **Include concrete examples** - Real usage patterns
- **Show relationships** - How components interact
- **Document decisions** - Architectural choices and rationale

---

## Documentation Templates

### 1. README.md - Project Overview

```markdown
# [Project Name]

[![License]][License URL]
[![Language]][Language Stats]

## Overview

[Brief 2-3 sentence description of what this project does and its main value proposition]

## Features

- ✅ [Feature 1] - [Brief description]
- ✅ [Feature 2] - [Brief description]
- ✅ [Feature 3] - [Brief description]

## Tech Stack

| Layer | Technology | Purpose |
|-------|------------|---------|
| Frontend | [React 18] | User interface |
| Backend | [Node.js + Express] | API server |
| Database | [PostgreSQL 15] | Primary data store |
| Cache | [Redis] | Session/cache layer |
| Queue | [RabbitMQ] | Async processing |

## Quick Start

### Prerequisites

- [Requirement 1]
- [Requirement 2]
- [Requirement 3]

### Installation

```bash
# Clone the repository
git clone https://github.com/org/repo.git
cd repo

# Install dependencies
npm install

# Setup environment
cp .env.example .env
# Edit .env with your configuration

# Run development server
npm run dev
```

### Usage

```typescript
// Example: How to use the main functionality
import { Client } from './src/client';

const client = new Client({ apiKey: process.env.API_KEY });
const result = await client.processData(input);
console.log(result);
```

## Architecture

See [ARCHITECTURE.md](ARCHITECTURE.md) for detailed system design.

## API Reference

See [API.md](API.md) for complete API documentation.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for development guidelines.

## License

[License Name] - See [LICENSE](LICENSE) for details.
```

### 2. ARCHITECTURE.md - System Design

```markdown
# Architecture Documentation

## 1. System Overview

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        Client Layer                             │
│  ┌───────────┐  ┌───────────┐  ┌───────────┐                    │
│  │  Web App  │  │  Mobile   │  │   API     │                    │
│  └─────┬─────┘  └─────┬─────┘  └─────┬─────┘                    │
└────────┼──────────────┼──────────────┼─────────────────────────┘
         │              │              │
         └──────────────┴──────────────┘
                          │
                    ┌─────▼─────┐
                    │  Gateway  │
                    │  (Nginx)  │
                    └─────┬─────┘
                          │
         ┌────────────────┼────────────────┐
         │                │                │
   ┌─────▼─────┐    ┌─────▼─────┐    ┌─────▼─────┐
   │  Auth     │    │   API     │    │  Static   │
   │  Service  │    │  Server   │    │   Files   │
   └─────┬─────┘    └─────┬─────┘    └───────────┘
         │               │
         │      ┌────────┼────────┐
         │      │        │        │
         │   ┌──▼──┐  ┌──▼──┐  ┌──▼──┐
         │   │ Svc │  │ Svc │  │ Svc │
         │   │  A  │  │  B  │  │  C  │
         │   └─────┘  └─────┘  └─────┘
         │      │        │        │
         └──────┼────────┼────────┘
                │        │
         ┌──────┴────────┴──────┐
         │    Data Layer        │
   ┌─────┴─────┐  ┌─────────┐  ┌─────┐
   │ PostgreSQL│  │  Redis  │  │ S3  │
   └───────────┘  └─────────┘  └─────┘
```

### Architectural Patterns

| Pattern | Usage | Benefits |
|---------|-------|----------|
| [Pattern Name] | [Where applied] | [What benefit it provides] |

### Design Principles Applied

- **[Principle]:** [How it's applied in this codebase]
- **[Principle]:** [How it's applied in this codebase]

## 2. Component Architecture

### Component: [Name]

**Location:** `src/path/to/component`

**Purpose:** [What this component does and why it exists]

**Responsibilities:**
- [Responsibility 1]
- [Responsibility 2]
- [Responsibility 3]

**Dependencies:**
- [Internal]: [Module it depends on]
- [External]: [Package it depends on]

**Public Interface:**
```typescript
// Main class/function exported
export class ComponentName {
  constructor(config: Config): void
  method1(params: Type): Promise<Result>
  method2(params: Type): Result
}
```

### Component Relationships

```
[Component A] ─────► [Component B]
   │                    │
   │                    ▼
   └─────────► [Component C]
```

## 3. Data Flow Architecture

### Data Flow: [Flow Name]

**Description:** [What this flow accomplishes]

**Steps:**
```
1. [Trigger] → [Entry Point]
2. [Entry Point] validates input and creates [Request]
3. [Service Layer] processes business logic
4. [Data Access] persists/retrieves from [Store]
5. [Response] formatted and returned
```

**Data Transformations:**
| Stage | Input | Output | Transformation |
|-------|-------|--------|----------------|
| Validation | Raw input | Validated object | Sanitize & validate |
| Processing | Validated object | Domain model | Business rules applied |
| Storage | Domain model | DB record | ORM mapping |

## 4. Module Dependency Graph

```
src/
├── core/                    # Core domain logic
│   ├── models/            # Domain models
│   ├── services/          # Business services
│   └── utils/             # Core utilities
├── modules/               # Feature modules
│   ├── auth/              # Authentication
│   ├── users/             # User management
│   └── payments/          # Payment processing
├── infrastructure/        # External integrations
│   ├── database/          # DB connection & repos
│   ├── cache/            # Redis integration
│   └── queue/             # Message queue setup
└── api/                   # API layer
    ├── routes/            # Express/Fastify routes
    ├── controllers/       # Request handlers
    └── middleware/        # Shared middleware
```

### Dependency Analysis

**Most Coupled Modules:**
- `payments` ↔ `users` - [Why they're coupled]
- `notifications` ↔ `core/services` - [Why they're coupled]

**Most Stable/Independent:**
- `utils` - No external dependencies
- `core/types` - Pure definitions

## 5. Design Decisions

### Decision: [Decision Title]

**Context:** [What situation prompted this decision]

**Options Considered:**
1. [Option A] - [Pros/Cons]
2. [Option B] - [Pros/Cons]
3. [Option C] - [Pros/Cons]

**Chosen Solution:** [What was chosen]

**Rationale:** [Why this was the best choice]

**Implications:**
- [Positive]: [Benefit]
- [Trade-off]: [What was sacrificed]

## 6. Security Architecture

### Authentication Flow

```
User Login Request
       │
       ▼
┌──────────────────┐
│  Validate creds │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ Generate JWT     │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ Set HTTP-only   │
│ Cookie          │
└──────────────────┘
```

### Security Measures

| Layer | Measure | Implementation |
|-------|---------|----------------|
| Transport | TLS 1.3 | All HTTPS |
| Auth | JWT | 15-min expiry + refresh |
| Validation | Zod | Schema validation on all inputs |
| Database | Parameterized queries | ORM prevents injection |

## 7. Scalability & Performance

### Horizontal Scaling

- **Stateless design** allows easy scaling
- **Redis session store** for distributed sessions
- **Read replicas** for database scaling

### Performance Optimizations

| Optimization | Location | Impact |
|--------------|----------|--------|
| [Optimization] | [Where applied] | [What improvement] |
```

### 3. API.md - Complete API Reference

```markdown
# API Reference

## Overview

This document provides complete API documentation for all public interfaces, endpoints, and data types.

## Table of Contents

- [Authentication](#authentication)
- [Users](#users)
- [Resources](#resources)
- [Webhooks](#webhooks)
- [Data Types](#data-types)

---

## Authentication

### Bearer Token Authentication

All API requests require a valid JWT token in the Authorization header:

```http
Authorization: Bearer <your-jwt-token>
```

Token validation middleware: `src/api/middleware/auth.ts`

---

## Users

### UserService

**Location:** `src/modules/users/user.service.ts`

```typescript
class UserService {
  /**
   * Create a new user account
   * @param data - User creation data
   * @returns Created user (without password)
   * @throws UserAlreadyExistsError - If email already registered
   */
  async create(data: CreateUserDTO): Promise<UserResponse>

  /**
   * Find user by ID
   * @param id - User's UUID
   * @returns User if found
   * @throws UserNotFoundError - If user doesn't exist
   */
  async findById(id: string): Promise<UserResponse>

  /**
   * Update user profile
   * @param id - User's UUID
   * @param data - Update data (partial)
   * @returns Updated user
   */
  async update(id: string, data: UpdateUserDTO): Promise<UserResponse>

  /**
   * Soft delete user account
   * @param id - User's UUID
   */
  async delete(id: string): Promise<void>
}
```

#### `create(data: CreateUserDTO): Promise<UserResponse>`

**Signature:**
```typescript
create(data: CreateUserDTO): Promise<UserResponse>
```

**Parameters:**

| Name | Type | Required | Description |
|------|------|----------|-------------|
| data | `CreateUserDTO` | Yes | User creation payload |

**Request Body (`CreateUserDTO`):**
```typescript
{
  email: string;        // User's email address (unique)
  name: string;         // Display name (2-100 chars)
  password: string;     // Min 8 chars, must include number
  role?: 'user'|'admin' // Default: 'user'
}
```

**Response (`UserResponse`):**
```typescript
{
  id: string;           // UUID v4
  email: string;
  name: string;
  role: 'user'|'admin';
  createdAt: string;    // ISO 8601 timestamp
  updatedAt: string;    // ISO 8601 timestamp
}
```

**Example:**
```typescript
// Request
const user = await userService.create({
  email: 'john@example.com',
  name: 'John Doe',
  password: 'secure123'
});

// Response
{
  id: '550e8400-e29b-41d4-a716-446655440000',
  email: 'john@example.com',
  name: 'John Doe',
  role: 'user',
  createdAt: '2024-01-15T10:30:00Z',
  updatedAt: '2024-01-15T10:30:00Z'
}
```

**Errors:**
- `400 Bad Request` - Invalid input data
- `409 Conflict` - Email already exists

---

## Resources

### ResourceController

**Location:** `src/modules/resources/resource.controller.ts`

Endpoints:

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/resources` | List all resources |
| POST | `/api/resources` | Create new resource |
| GET | `/api/resources/:id` | Get resource by ID |
| PUT | `/api/resources/:id` | Update resource |
| DELETE | `/api/resources/:id` | Delete resource |

#### `GET /api/resources`

**Query Parameters:**

| Name | Type | Required | Description |
|------|------|----------|-------------|
| page | number | No | Page number (default: 1) |
| limit | number | No | Items per page (default: 20, max: 100) |
| sort | string | No | Sort field (createdAt, name) |
| order | 'asc'\|'desc' | No | Sort order |

**Response:**
```typescript
{
  data: Resource[];
  meta: {
    total: number;
    page: number;
    limit: number;
    totalPages: number;
  }
}
```

#### `POST /api/resources`

**Request Body:**
```typescript
{
  name: string;
  type: 'document'|'image'|'video';
  url: string;         // Valid URL
  metadata?: Record<string, unknown>;
}
```

---

## Webhooks

### Outgoing Webhooks

**Location:** `src/integrations/webhooks/webhook.service.ts`

#### Events

| Event | Payload | Trigger |
|-------|---------|---------|
| `user.created` | `UserResponse` | New user registration |
| `resource.created` | `ResourceResponse` | New resource upload |
| `order.completed` | `OrderResponse` | Payment successful |

#### Signature
```typescript
interface WebhookPayload<T = unknown> {
  id: string;           // Event ID (UUID)
  event: string;        // Event name
  timestamp: string;    // ISO 8601
  data: T;              // Event data
}
```

---

## Data Types

### Core Types

```typescript
// Common pagination
interface PaginationParams {
  page?: number;
  limit?: number;
  sort?: string;
  order?: 'asc' | 'desc';
}

interface PaginatedResponse<T> {
  data: T[];
  meta: {
    total: number;
    page: number;
    limit: number;
    totalPages: number;
  };
}

// Error response
interface ApiError {
  code: string;
  message: string;
  details?: Record<string, unknown>;
}
```

### Domain Types

```typescript
// User domain model
interface User {
  id: string;
  email: string;
  name: string;
  role: 'user' | 'admin';
  createdAt: Date;
  updatedAt: Date;
}
```

---

## Error Codes

| Code | HTTP Status | Description |
|------|-------------|-------------|
| `VALIDATION_ERROR` | 400 | Invalid input data |
| `NOT_FOUND` | 404 | Resource doesn't exist |
| `UNAUTHORIZED` | 401 | Missing/invalid token |
| `FORBIDDEN` | 403 | Insufficient permissions |
| `CONFLICT` | 409 | Resource already exists |
| `INTERNAL_ERROR` | 500 | Server error |
```

### 4. MODULES.md - Module Breakdown

```markdown
# Module Documentation

## Module Overview

| Module | Location | Purpose | Key Exports |
|--------|----------|---------|-------------|
| core | `src/core/` | Domain models and business logic | `User`, `Order`, `Validation` |
| auth | `src/modules/auth/` | Authentication & authorization | `AuthService`, `Guard` |
| users | `src/modules/users/` | User management | `UserService`, `UserController` |
| payments | `src/modules/payments/` | Payment processing | `PaymentService`, `Provider` |

---

## Core Module

**Path:** `src/core/`

### Purpose

Contains the domain layer - pure business logic independent of frameworks, databases, or external services. This is the heart of the application.

### Files

| File | Purpose | Exports |
|------|---------|---------|
| `models/` | Domain entities and aggregates | `User`, `Order`, `Product` |
| `value-objects/` | Immutable value objects | `Email`, `Money`, `Address` |
| `events/` | Domain events | `UserCreated`, `OrderPlaced` |
| `exceptions/` | Domain exceptions | `DomainError`, `ValidationError` |

### Domain Model: User

```typescript
// src/core/models/user.ts

export class User extends AggregateRoot {
  constructor(
    public readonly id: UserId,
    public readonly email: Email,
    public readonly name: UserName,
    private _passwordHash: PasswordHash,
    public readonly role: UserRole,
    public readonly createdAt: DateTime
  ) {
    super();
  }

  /**
   * Create a new user from raw data
   * @throws ValidationError if data is invalid
   */
  static create(data: CreateUserInput): User {
    // Business logic: Validate email format, hash password
    // Emit UserCreated domain event
    return new User(
      UserId.generate(),
      Email.fromString(data.email),
      UserName.fromString(data.name),
      await PasswordHash.fromPlain(data.password),
      data.role ?? UserRole.USER,
      DateTime.now()
    );
  }

  /**
   * Check if provided password matches stored hash
   */
  async verifyPassword(plain: string): Promise<boolean> {
    return bcrypt.compare(plain, this._passwordHash.value);
  }

  // Domain methods
  public changeName(newName: UserName): void {
    this.addDomainEvent(new UserNameChanged(this.id, this.name, newName));
    this.name = newName;
  }
}
```

### Value Object: Email

```typescript
// src/core/value-objects/email.ts

export class Email extends ValueObject {
  constructor(private readonly _value: string) {
    super();
    if (!Email.isValid(_value)) {
      throw new ValidationError('Invalid email format');
    }
  }

  static fromString(value: string): Email {
    return new Email(value.toLowerCase().trim());
  }

  private static isValid(email: string): boolean {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return emailRegex.test(email);
  }

  get value(): string {
    return this._value;
  }
}
```

### Business Rules Enforced

1. **User email must be unique** - Checked in repository before persistence
2. **Password minimum strength** - 8 chars, number, special char
3. **Orders cannot exceed stock** - Verified at order placement

---

## Auth Module

**Path:** `src/modules/auth/`

### Architecture

```
src/modules/auth/
├── auth.service.ts      # Main authentication logic
├── strategies/          # Passport/Auth.js strategies
│   ├── jwt.strategy.ts
│   └── local.strategy.ts
├── guards/              # Route guards
│   └── auth.guard.ts
└── tokens/               # Token management
    ├── token.service.ts
    └── refresh-token.repository.ts
```

### AuthService

**Signature:**
```typescript
class AuthService {
  async login(credentials: LoginDTO): Promise<AuthResponse>
  async register(data: RegisterDTO): Promise<AuthResponse>
  async refreshToken(refreshToken: string): Promise<AuthResponse>
  async validateUser(userId: string): Promise<User | null>
}
```

### Authentication Flow

```typescript
// Login sequence
async login({ email, password }: LoginDTO): Promise<AuthResponse> {
  // 1. Find user by email
  const user = await this.userRepository.findByEmail(email);
  
  // 2. Verify password
  if (!await user.verifyPassword(password)) {
    throw new UnauthorizedError('Invalid credentials');
  }
  
  // 3. Check user is active
  if (!user.isActive) {
    throw new ForbiddenError('Account is deactivated');
  }
  
  // 4. Generate tokens
  const accessToken = this.jwtService.sign({ sub: user.id });
  const refreshToken = await this.tokenService.generateRefresh(user.id);
  
  // 5. Return auth response
  return { accessToken, refreshToken, user: user.toResponse() };
}
```

---

## Payments Module

**Path:** `src/modules/payments/`

### Responsibility

Handles all payment-related operations including:
- Payment processing with multiple providers
- Refund handling
- Payment verification
- Transaction history

### Key Classes

| Class | Purpose |
|-------|---------|
| `PaymentService` | Orchestrates payment operations |
| `PaymentProvider` | Interface for provider implementations |
| `StripeProvider` | Stripe integration |
| `PayPalProvider` | PayPal integration |
| `RefundService` | Handles refund workflows |

### Payment Flow Diagram

```
┌─────────────────┐
│ Client initiates │
│   payment       │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ PaymentService  │
│ validates order │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ ProviderFactory │
│ selects provider│
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ PaymentProvider │
│ calls external  │
│ API             │
└────────┬────────┘
         │
    ┌────┴────┐
    │         │
    ▼         ▼
┌───────┐ ┌───────┐
│Success│ │ Failure│
└───┬───┘ └───┬───┘
    │         │
    ▼         ▼
┌───────────────────────┐
│ Update order status   │
│ Emit PaymentCompleted │
│ or PaymentFailed      │
└───────────────────────┘
```

### Provider Interface

```typescript
interface PaymentProvider {
  /**
   * Process a payment
   * @param amount - Payment amount
   * @param currency - ISO currency code
   * @param metadata - Additional data
   * @returns Payment result with transaction ID
   */
  processPayment(
    amount: Money,
    currency: string,
    metadata: PaymentMetadata
  ): Promise<PaymentResult>;

  /**
   * Process a refund
   * @param transactionId - Original transaction ID
   * @param amount - Amount to refund (partial or full)
   * @returns Refund result
   */
  processRefund(
    transactionId: string,
    amount?: Money
  ): Promise<RefundResult>;

  /**
   * Verify payment status
   * @param transactionId - Transaction to verify
   */
  verifyPayment(transactionId: string): Promise<PaymentStatus>;
}
```

### Configuration

```typescript
// src/modules/payments/config.ts
export const paymentConfig = {
  providers: ['stripe', 'paypal'],
  defaultProvider: 'stripe',
  stripe: {
    apiKey: process.env.STRIPE_SECRET_KEY,
    webhookSecret: process.env.STRIPE_WEBHOOK_SECRET,
  },
  paypal: {
    clientId: process.env.PAYPAL_CLIENT_ID,
    clientSecret: process.env.PAYPAL_CLIENT_SECRET,
  },
};
```

---

## Module Dependencies

```
┌─────────────────────────────────────────────────────────────┐
│                        core/                                │
│   ┌─────────┐  ┌─────────┐  ┌─────────┐                    │
│   │ models  │  │ events  │  │  rules  │                    │
│   └────┬────┘  └────┬────┘  └────┬────┘                    │
│        │            │            │                          │
│        └────────────┴────────────┘                          │
└─────────────────────────────────────────────────────────────┘
                           │
           ┌───────────────┼───────────────┐
           │               │               │
    ┌──────▼──────┐ ┌──────▼──────┐ ┌──────▼──────┐
    │    auth/    │ │   users/    │ │  payments/  │
    │             │ │             │ │             │
    │ Depends on: │ │ Depends on: │ │ Depends on: │
    │ - core/user │ │ - core/user │ │ - core/order│
    └─────────────┘ └─────────────┘ └─────────────┘
```

---

## Module Patterns

### Service Pattern

All modules follow the service pattern:

```
[Module]Service
├── [Module]Repository (interface)
├── [Module]Controller (if HTTP)
├── DTOs/
│   ├── Create[Module]DTO
│   ├── Update[Module]DTO
│   └── [Module]Response
└── [Module].entity.ts
```

### Repository Pattern

```typescript
// Interface defines contract
interface UserRepository {
  findById(id: string): Promise<User | null>;
  findByEmail(email: string): Promise<User | null>;
  save(user: User): Promise<void>;
  delete(id: string): Promise<void>;
}

// Implementation for specific DB
class PostgresUserRepository implements UserRepository {
  // Prisma/TypeORM implementation
}
```
```

### 5. FILE_INVENTORY.md - Complete File List

```markdown
# File Inventory

## Summary

| Category | Count |
|----------|-------|
| Total Files | [N] |
| Source Files | [N] |
| Test Files | [N] |
| Config Files | [N] |
| Documentation | [N] |

## Directory Structure

```
project-root/
├── .github/                  # GitHub workflows
│   └── workflows/
│       ├── ci.yml
│       └── release.yml
├── src/
│   ├── api/                  # API layer
│   │   ├── controllers/
│   │   ├── routes/
│   │   └── middleware/
│   ├── core/                 # Domain layer
│   │   ├── models/
│   │   ├── value-objects/
│   │   ├── events/
│   │   └── exceptions/
│   ├── modules/              # Feature modules
│   │   ├── auth/
│   │   ├── users/
│   │   └── payments/
│   ├── infrastructure/       # External integrations
│