# Adventure Works Frontend - Angular Application

This directory contains the Angular 17+ frontend application with feature-based architecture.

## Project Structure

### 🏗️ Application Architecture

```
src/app/
├── core/                    # Singleton services and guards
├── shared/                  # Reusable components and pipes
├── features/               # Feature modules (lazy-loaded)
│   ├── products/           # Product catalog features
│   ├── cart/              # Shopping cart features  
│   ├── checkout/          # Checkout process
│   └── user/              # User profile and auth
├── state/                 # NgRx global state management
└── models/                # TypeScript interfaces and types
```

### 📁 Directory Descriptions

#### core/
- **Purpose**: App-wide singleton services and route guards  
- **Contains**: HTTP interceptors, auth guards, core services
- **Examples**: AuthService, HttpInterceptor, RouteGuard

#### shared/
- **Purpose**: Reusable components used across features
- **Contains**: Common components, pipes, directives
- **Examples**: LoadingSpinner, ConfirmDialog, CurrencyPipe

#### features/
- **Purpose**: Self-contained feature modules
- **Structure**: Each feature has components, services, and routing
- **Benefits**: Lazy loading, maintainability, team collaboration

#### state/
- **Purpose**: Global application state with NgRx
- **Contains**: Actions, reducers, effects, selectors
- **Examples**: Product state, cart state, user state

#### models/
- **Purpose**: TypeScript interfaces and type definitions
- **Contains**: API response models, form models, enums
- **Examples**: Product interface, User interface, OrderStatus enum

## Development Guidelines

- **Lazy Loading**: Feature modules are lazy-loaded for performance
- **OnPush**: Use OnPush change detection strategy  
- **Reactive**: Prefer reactive programming with RxJS
- **Material Design**: Use Angular Material components
- **Responsive**: Mobile-first responsive design