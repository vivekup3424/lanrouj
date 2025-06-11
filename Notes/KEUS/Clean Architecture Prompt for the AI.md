## Overview

This guideline defines the clean architecture pattern used by our organization. Follow this structure when refactoring applications to ensure consistency, maintainability, and adherence to SOLID principles.

## Directory Structure

### 1. Application Layer (`/application`)

**Purpose**: Orchestrates business logic and handles external interactions

#### Structure:

- **`/controllers`**: Handle incoming requests and coordinate responses
    
    - **Specific controllers**: Feature-specific request handlers
- **`/gateways`**: External system interfaces and API gateways
    
    - **API gateways**: REST/GraphQL endpoint definitions
    - **Message brokers**: Event streaming and messaging interfaces

#### Guidelines:

- Controllers should be thin - delegate business logic to use cases
- Each controller handles one specific concern or feature
- Gateways abstract external service communications
- No direct database access - use repositories via dependency injection

### 2. Core Layer (`/core`)

**Purpose**: Contains cross-cutting concerns and shared utilities

#### Structure:

- **`/config`**: Configuration management (environment-specific settings)
- **`/constants`**: Application-wide constants and enums
- **`/errors`**: Custom error types and error handling utilities
- **`/startup`**: Application initialization and bootstrap logic
- **`/utils`**: Pure utility functions (no business logic dependencies)

#### Guidelines:

- Keep utilities pure and stateless where possible
- Configuration should be environment-aware
- Error types should be specific and descriptive
- No business logic in this layer

### 3. Domain Layer (`/domain`)

**Purpose**: Contains business logic, entities, and defines contracts

#### Structure:

- **`/entities`**: Business objects and domain models
    
    - Rich domain objects with behavior
    - No external dependencies
    - Represent core business concepts
- **`/repositories`**: Data access contracts (interfaces only)
    
    - Define what data operations are needed
    - No implementation details
    - Return domain entities
- **`/use-cases`**: Business logic implementation
    
    - **Organize by feature/domain**: `agent-use-cases/`, `gateway-use-cases/`
    - Each use case represents one business operation
    - Coordinate between entities and repositories

#### Guidelines:

- Entities should contain business rules and validation
- Repository interfaces define contracts, not implementations
- Use cases orchestrate business workflows
- No framework dependencies in this layer
- Use cases should have single responsibility

### 4. Infrastructure Layer (`/infrastructure`)

**Purpose**: Implements external concerns and technical details

#### Structure:

- **`/adapters`**: External service implementations
    
    - Third-party service integrations
    - Protocol-specific implementations (HTTP, message queues)
- **`/data`**: Data access implementations
    
    - **`/models`**: Data transfer objects and database schemas
    - **`/repositories`**: Concrete repository implementations
    - Database-specific logic
- **`/event-listeners`**: Event handling implementations
    
- **`/helpers`**: Infrastructure-specific utility functions
    
- **`/managers`**: System-level service managers
    

#### Guidelines:

- Repository implementations contain data access logic
- Models are for data transfer, not business logic
- Adapters implement domain interfaces
- Managers handle system-level concerns (connections, lifecycle)
- All external dependencies isolated here

### 5. Dependency Injection (`/di`)

**Purpose**: Manages object creation and dependency wiring

#### Structure:

- **`bootstrap.ts`**: Application startup and container configuration
- **`interface.ts`**: Dependency injection contracts
- **`index.ts`**: Container exports and public interface

#### Guidelines:

- Use dependency injection container for loose coupling
- Register all dependencies at application startup
- Interface segregation for testability

## Refactoring Principles

### 1. Dependency Direction

- **Inward dependencies only**: Domain ← Application ← Infrastructure
- Domain layer has no external dependencies
- Use dependency inversion for infrastructure concerns

### 2. Separation of Concerns

- **Controllers**: Request/response handling, input validation
- **Use Cases**: Business logic coordination
- **Entities**: Business rules and domain behavior
- **Repositories**: Data access abstraction
- **Infrastructure**: Technical implementation details

### 3. Interface Segregation

- Create specific interfaces for each concern
- Avoid god interfaces
- Repository interfaces should be focused on single entity types

### 4. Single Responsibility

- Each class/module has one reason to change
- Use cases handle one business operation
- Controllers handle one endpoint/event type

### 5. Naming Conventions

- **Controllers**: `{feature}-controller` or `{domain}-{type}-controller`
- **Use Cases**: `{action}-{entity}-usecase`
- **Repositories**: `{entity}-repo-interface` (domain), `{entity}-repo-impl` (infrastructure)
- **Entities**: Business domain names (e.g., `agent`, `gateway`)

## Migration Strategy

### Phase 1: Structure Setup

1. Create the four main directories
2. Move existing code to appropriate layers
3. Identify and separate concerns

### Phase 2: Domain Extraction

1. Extract business entities from data models
2. Create repository interfaces
3. Implement use cases for business logic

### Phase 3: Infrastructure Isolation

1. Move external dependencies to infrastructure layer
2. Create adapters for third-party services
3. Implement repository concrete classes

### Phase 4: Dependency Injection

1. Set up DI container
2. Wire dependencies through interfaces
3. Remove direct dependencies between layers

## Validation Checklist

- [ ] No business logic in controllers
- [ ] Domain entities have no external dependencies
- [ ] Repository interfaces defined in domain layer
- [ ] All external services accessed through adapters
- [ ] Use cases coordinate business workflows
- [ ] Dependencies flow inward only
- [ ] Each layer has clear responsibilities
- [ ] Infrastructure implementations are swappable

## Common Pitfalls to Avoid

1. **Anemic Domain Models**: Entities should contain behavior, not just data
2. **Fat Controllers**: Move business logic to use cases
3. **Direct Database Access**: Always use repository abstractions
4. **Circular Dependencies**: Maintain proper dependency direction
5. **God Classes**: Keep classes focused on single responsibilities
6. **Tight Coupling**: Use interfaces and dependency injection
7. **Mixed Concerns**: Don't mix business logic with infrastructure code

This architecture ensures testability, maintainability, and clear separation of concerns while enabling independent evolution of different layers.