# Adventure Works Backend - Clean Architecture

This directory contains the backend ASP.NET Core 8.0 Web API implementation following Clean Architecture principles.

## Project Structure

### 🏗️ Architecture Layers

```
src/
├── AdventureWorks.Domain/           # Domain Layer
├── AdventureWorks.Application/      # Application Layer  
├── AdventureWorks.Infrastructure/   # Infrastructure Layer
└── AdventureWorks.API/             # Presentation Layer
```

### 📁 Layer Descriptions

#### AdventureWorks.Domain/
- **Purpose**: Core business entities and domain logic
- **Contains**: Entities, Value Objects, Domain Events, Interfaces
- **Dependencies**: None (pure domain logic)
- **Examples**: Product, Customer, Order entities

#### AdventureWorks.Application/
- **Purpose**: Business use cases and application logic
- **Contains**: CQRS Commands/Queries, DTOs, Validators, Interfaces
- **Dependencies**: Domain layer only
- **Examples**: CreateOrderCommand, GetProductsQuery

#### AdventureWorks.Infrastructure/  
- **Purpose**: External concerns and data persistence
- **Contains**: DbContext, Repositories, External API clients
- **Dependencies**: Application and Domain layers
- **Examples**: EF Core DbContext, Email service, Payment gateway

#### AdventureWorks.API/
- **Purpose**: Web API controllers and middleware
- **Contains**: Controllers, Middleware, Configuration
- **Dependencies**: All other layers
- **Examples**: ProductsController, AuthController

## Key Principles

- **Dependency Inversion**: Dependencies point inward toward the domain
- **Separation of Concerns**: Each layer has a specific responsibility  
- **Testability**: Business logic is isolated and easily testable
- **Independence**: Domain logic is framework-independent