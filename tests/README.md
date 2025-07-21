# Adventure Works Backend Tests

This directory contains the test suites for the Adventure Works backend API.

## Test Structure

```
tests/
├── AdventureWorks.UnitTests/           # Unit tests
└── AdventureWorks.IntegrationTests/    # Integration tests
```

## Test Categories

### Unit Tests
- **Purpose**: Test individual components in isolation
- **Scope**: Services, repositories, domain logic, validators
- **Tools**: xUnit, Moq, FluentAssertions
- **Coverage Target**: 80%+ code coverage

### Integration Tests
- **Purpose**: Test component interactions and API endpoints  
- **Scope**: Controllers, database operations, external services
- **Tools**: WebApplicationFactory, TestContainers, InMemory DB
- **Focus**: End-to-end request/response flows

## Testing Guidelines

### Unit Test Best Practices
- Use descriptive test method names
- Follow AAA pattern (Arrange, Act, Assert)
- Mock external dependencies
- Test both success and failure scenarios

### Integration Test Best Practices  
- Use realistic test data
- Clean up test data after each test
- Test authentication and authorization
- Validate API contracts and response formats

### Test Organization
- Mirror the source code structure
- Group related tests in test classes
- Use test categories for different test types
- Maintain test data builders for complex objects