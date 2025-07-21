# Claude.md - Adventure Works E-Commerce Project Guide

## Project Overview

You are working on an e-commerce web application for Adventure Works. This is a modern, minimalist online shopping platform with a C# ASP.NET Core backend API and an Angular frontend.

### Core Principles
- **Design**: Clean, minimalist, and beautiful UI
- **Architecture**: Clean Architecture with CQRS pattern
- **User Experience**: Intuitive, efficient, and accessible
- **Code Quality**: Maintainable, testable, and scalable

## Technical Stack

### Backend (C# ASP.NET Core)
- **Framework**: ASP.NET Core 8.0
- **Database**: SQL Server with Adventure Works schema
- **ORM**: Entity Framework Core
- **Architecture**: Clean Architecture with CQRS
- **Authentication**: JWT with refresh tokens
- **API Documentation**: Swagger/OpenAPI
- **Caching**: Redis

### Frontend (Angular)
- **Framework**: Angular 17+
- **State Management**: NgRx
- **UI Library**: Angular Material (custom themed)
- **Styling**: SCSS with CSS Grid/Flexbox
- **Testing**: Jasmine/Karma (unit), Cypress (E2E)

## Project Structure

### Backend Structure
```
AdventureWorks.API/
├── src/
│   ├── AdventureWorks.Domain/          # Domain entities and interfaces
│   ├── AdventureWorks.Application/     # Business logic, CQRS handlers
│   ├── AdventureWorks.Infrastructure/  # Data access, external services
│   └── AdventureWorks.API/            # Controllers, middleware
├── tests/
│   ├── AdventureWorks.UnitTests/
│   └── AdventureWorks.IntegrationTests/
```

### Frontend Structure
```
adventure-works-ui/
├── src/
│   ├── app/
│   │   ├── core/                      # Singleton services, guards
│   │   ├── shared/                    # Shared components, pipes
│   │   ├── features/                  # Feature modules
│   │   │   ├── products/
│   │   │   ├── cart/
│   │   │   ├── checkout/
│   │   │   └── user/
│   │   ├── state/                     # NgRx store
│   │   └── models/                    # TypeScript interfaces
│   ├── assets/
│   └── styles/                        # Global SCSS
```

## Database Context

Using Adventure Works database with key tables:
- **Production.Product**: Products catalog
- **Production.ProductCategory**: Category hierarchy
- **Sales.Customer**: Customer information
- **Sales.SalesOrderHeader**: Order headers
- **Sales.SalesOrderDetail**: Order line items
- **Production.ProductPhoto**: Product images
- **Production.ProductInventory**: Stock levels

## API Endpoints Pattern

All APIs follow RESTful conventions:
- Base URL: `/api`
- Versioning: `/api/v1`
- Response format: JSON
- Status codes: Standard HTTP codes
- Error format: `{ "error": { "code": "string", "message": "string", "details": {} } }`

### Authentication Headers
```
Authorization: Bearer {jwt_token}
```

## Code Standards

### C# Backend
```csharp
// Use explicit types for clarity
public async Task<ActionResult<ProductDto>> GetProduct(int id)
{
    // Use early returns for validation
    if (id <= 0)
        return BadRequest("Invalid product ID");
    
    // Use dependency injection
    var product = await _productService.GetByIdAsync(id);
    
    // Use DTOs for API responses
    return Ok(_mapper.Map<ProductDto>(product));
}
```

### Angular Frontend
```typescript
// Use strong typing
export interface Product {
  id: number;
  name: string;
  price: number;
  imageUrl: string;
}

// Use reactive programming
getProducts(): Observable<Product[]> {
  return this.http.get<Product[]>(`${this.apiUrl}/products`).pipe(
    map(products => products),
    catchError(this.handleError)
  );
}
```

## Design System

### Colors
```scss
// Primary palette
$primary: #1976d2;
$primary-light: #63a4ff;
$primary-dark: #004ba0;

// Neutral palette
$gray-100: #f5f5f5;
$gray-200: #eeeeee;
$gray-300: #e0e0e0;
$gray-400: #bdbdbd;
$gray-500: #9e9e9e;
$gray-600: #757575;
$gray-700: #616161;
$gray-800: #424242;
$gray-900: #212121;

// Semantic colors
$success: #4caf50;
$warning: #ff9800;
$error: #f44336;
```

### Typography
```scss
// Font family
$font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;

// Font sizes
$font-size-xs: 0.75rem;    // 12px
$font-size-sm: 0.875rem;   // 14px
$font-size-base: 1rem;     // 16px
$font-size-lg: 1.125rem;   // 18px
$font-size-xl: 1.25rem;    // 20px
$font-size-2xl: 1.5rem;    // 24px
$font-size-3xl: 1.875rem;  // 30px
```

### Spacing
```scss
$spacing-unit: 8px;
$spacing-xs: $spacing-unit * 0.5;   // 4px
$spacing-sm: $spacing-unit;         // 8px
$spacing-md: $spacing-unit * 2;     // 16px
$spacing-lg: $spacing-unit * 3;     // 24px
$spacing-xl: $spacing-unit * 4;     // 32px
$spacing-2xl: $spacing-unit * 6;    // 48px
```

## Common Patterns

### API Response Handling
```typescript
// Service method
getProducts(params?: ProductParams): Observable<PagedResult<Product>> {
  return this.http.get<PagedResult<Product>>(`${this.apiUrl}/products`, { params })
    .pipe(
      tap(result => console.log('Products loaded', result)),
      catchError(this.handleError<PagedResult<Product>>('getProducts'))
    );
}
```

### State Management (NgRx)
```typescript
// Action
export const loadProducts = createAction('[Product List] Load Products');
export const loadProductsSuccess = createAction(
  '[Product List] Load Products Success',
  props<{ products: Product[] }>()
);

// Effect
loadProducts$ = createEffect(() =>
  this.actions$.pipe(
    ofType(loadProducts),
    switchMap(() =>
      this.productService.getProducts().pipe(
        map(products => loadProductsSuccess({ products })),
        catchError(error => of(loadProductsFailure({ error })))
      )
    )
  )
);
```

### Error Handling
```csharp
// Global exception middleware
public class GlobalExceptionMiddleware
{
    public async Task InvokeAsync(HttpContext context, RequestDelegate next)
    {
        try
        {
            await next(context);
        }
        catch (Exception ex)
        {
            await HandleExceptionAsync(context, ex);
        }
    }
}
```

## Component Guidelines

### Product Card Component
- Display product image, name, price
- Show "Add to Cart" button on hover
- Include quick view option
- Responsive grid layout
- Lazy load images

### Cart Component
- Real-time updates
- Quantity adjustment
- Remove items
- Show subtotal
- Apply discount codes
- Persist across sessions

### Checkout Flow
1. Cart Review
2. Shipping Information
3. Payment Details
4. Order Confirmation
- Progress indicator
- Validation at each step
- Guest checkout option

## Performance Considerations

### Backend
- Use async/await for all I/O operations
- Implement response caching for product data
- Use pagination for list endpoints
- Include only necessary fields in DTOs
- Use database indexes on frequently queried columns

### Frontend
- Lazy load feature modules
- Use OnPush change detection
- Implement virtual scrolling for long lists
- Optimize images (WebP format, responsive sizes)
- Use trackBy functions in *ngFor
- Implement service workers for offline capability

## Security Guidelines

### Backend
- Validate all inputs
- Use parameterized queries
- Implement rate limiting
- Log security events
- Use HTTPS only
- Implement CORS properly
- Store passwords with bcrypt

### Frontend
- Sanitize user inputs
- Use Angular's built-in security features
- Implement CSP headers
- Avoid storing sensitive data in localStorage
- Use secure cookie flags

## Testing Strategy

### Unit Tests
- Aim for 80% code coverage
- Test all business logic
- Mock external dependencies
- Use descriptive test names

### Integration Tests
- Test API endpoints
- Test database operations
- Test authentication flow
- Use in-memory database for tests

### E2E Tests
- Test critical user paths
- Test checkout flow
- Test search functionality
- Run on multiple browsers

## Deployment Checklist

### Backend
- [ ] Environment variables configured
- [ ] Connection strings secured
- [ ] Logging configured
- [ ] Health checks implemented
- [ ] Swagger disabled in production
- [ ] CORS configured correctly

### Frontend
- [ ] Production build created
- [ ] Environment files configured
- [ ] Source maps disabled
- [ ] Bundle size optimized
- [ ] CDN configured
- [ ] SSL certificates valid

## Common Issues and Solutions

### Issue: Slow product loading
**Solution**: Implement Redis caching, optimize queries, add indexes

### Issue: Cart sync issues
**Solution**: Use WebSocket for real-time updates, implement optimistic UI

### Issue: Payment failures
**Solution**: Implement retry logic, provide clear error messages

### Issue: Mobile performance
**Solution**: Lazy load images, reduce bundle size, use PWA features

## Future Enhancements

When asked about new features, consider:
- Progressive Web App capabilities
- AI-powered recommendations
- Wishlist functionality
- Product reviews and ratings
- Advanced search with filters
- Social login options
- Multi-language support
- A/B testing infrastructure

## Key Commands for Development

### Backend
```bash
# Run locally
dotnet run --project src/AdventureWorks.API

# Run tests
dotnet test

# EF migrations
dotnet ef migrations add MigrationName
dotnet ef database update
```

### Frontend
```bash
# Development server
ng serve

# Build production
ng build --prod

# Run tests
ng test
ng e2e

# Generate component
ng generate component features/products/product-list
```

## Remember

1. Always maintain the minimalist design aesthetic
2. Follow Clean Architecture principles
3. Write testable, maintainable code
4. Consider performance implications
5. Ensure accessibility (WCAG 2.1 AA)
6. Keep security as a top priority
7. Document complex logic
8. Use consistent naming conventions
9. Implement proper error handling
10. Think mobile-first