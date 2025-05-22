# AI Coding Rules for Kotlin, Spring Boot 3 & AWS Development

This document defines the rules and guidelines for AI-assisted code generation in our development environment. These rules should be followed when working with AI agents for code generation to ensure consistency, quality, and adherence to our stack and architecture.

## Technology Stack

### Primary Technologies
- **Kotlin** (latest stable version)
- **Spring Boot 3.x**
- **Gradle** for build management

### AWS Services
- **DynamoDB** for NoSQL database needs
- **SNS** (Simple Notification Service) for publish/subscribe messaging
- **SQS** (Simple Queue Service) for message queuing
- **EventBridge** for event-driven architectures
- **Parameter Store** for configuration management
- **Secrets Manager** for sensitive information

## Architecture Patterns

### REST API Applications
1. **Ports and Adapters / Hexagonal Architecture**:
   - Clear separation between domain logic and external dependencies
   - Domain models should be free from framework annotations
   - Use ports (interfaces) for dependency inversion
   - Implement adapters for external systems (databases, message queues, etc.)

2. **Project Structure**:
   ```
   src/main/kotlin/com/company/project/
   ├── domain/           # Domain models, business logic
   │   ├── model/        # Domain entities
   │   ├── service/      # Business services
   │   └── port/         # Interfaces for external dependencies
   ├── application/      # Application services, use cases
   │   ├── dto/          # Data Transfer Objects
   │   └── service/      # Application services
   ├── adapter/          # Implementations of ports
   │   ├── in/           # Inbound adapters (REST controllers)
   │   │   └── rest/     # REST controllers
   │   └── out/          # Outbound adapters (repositories, clients)
   │       ├── persistence/  # Database adapters
   │       └── messaging/    # Messaging adapters
   └── config/           # Configuration classes
   ```

### Background Services
1. **Three-Layer Architecture**:
   - **Presentation Layer**: Message consumers, event handlers
   - **Service Layer**: Business logic processing
   - **Data Access Layer**: Repositories, external service clients

2. **Project Structure**:
   ```
   src/main/kotlin/com/company/project/
   ├── consumer/         # Message/Event consumers
   ├── service/          # Business services
   │   ├── impl/         # Implementations
   │   └── model/        # Service models
   ├── repository/       # Data access layer
   │   ├── entity/       # Database entities
   │   └── impl/         # Repository implementations
   └── config/           # Configuration classes
   ```

## Coding Standards

### SOLID Principles
1. **Single Responsibility Principle**:
   - Each class should have only one reason to change
   - Keep classes focused and cohesive
   - Extract separate concerns into different classes

2. **Open/Closed Principle**:
   - Classes should be open for extension but closed for modification
   - Use interfaces and abstract classes for extension points
   - Prefer composition over inheritance

3. **Liskov Substitution Principle**:
   - Subtypes must be substitutable for their base types
   - Ensure implementations respect the contract of interfaces

4. **Interface Segregation Principle**:
   - Keep interfaces focused on specific client needs
   - Avoid "fat" interfaces; prefer multiple smaller interfaces

5. **Dependency Inversion Principle**:
   - High-level modules should not depend on low-level modules
   - Both should depend on abstractions
   - Use dependency injection (Spring's DI) extensively

### Kotlin-Specific Guidelines
1. **Utilize Kotlin Features**:
   - Use data classes for DTOs and value objects
   - Leverage extension functions for cleaner code
   - Use null safety features (avoid `!!` operator)
   - Prefer immutable collections and variables (`val` over `var`)

2. **Functional Programming**:
   - Use higher-order functions where appropriate
   - Apply collection transformations (map, filter, etc.) for clearer code
   - Consider using Kotlin coroutines for asynchronous programming

### Spring Boot Guidelines
1. **Configuration**:
   - Use configuration properties classes with `@ConfigurationProperties`
   - Externalize configuration to environment-specific files
   - Follow the 12-factor app methodology for configuration

2. **Dependency Injection**:
   - Use constructor injection over field injection
   - Prefer interfaces over concrete classes for dependencies

3. **API Design**:
   - Use REST best practices (proper HTTP verbs, status codes)
   - Implement consistent error handling with problem details
   - Version APIs appropriately

### AWS Integration
1. **Best Practices**:
   - Use Spring Cloud AWS when appropriate
   - Implement circuit breakers for AWS service calls
   - Follow least privilege principle for IAM roles

2. **Specific Services**:
   - **DynamoDB**: Use enhanced client with @DynamoDBTable annotations
   - **SNS/SQS**: Use Spring Cloud AWS messaging abstractions
   - **Parameter Store/Secrets Manager**: Integrate with Spring's PropertySource

## Testing Requirements

### Unit Testing
- Minimum 95% code coverage requirement
- Use JUnit 5 for testing
- Mockito or MockK for mocking dependencies
- Focus on testing business logic and edge cases
- Test one unit of functionality at a time

### Integration Testing
- Test interactions between components
- Use TestContainers for database/AWS service integration tests
- Verify proper wiring of components

### End-to-End Testing
- Test the complete flow of the application
- Cover critical user journeys
- Use Spring Boot Test for REST API testing

### Testing Structure
```
src/test/kotlin/com/company/project/
├── unit/              # Unit tests
├── integration/       # Integration tests
└── e2e/               # End-to-end tests
```

## Documentation Requirements

### REST API Documentation
- Create HTTP files for each endpoint with examples
- Example location: `/docs/http/endpoints.http`
- Include sample requests and responses
- Document error scenarios

### README Requirements
The project README must include:
1. **Project Overview**
   - Purpose and scope of the application
   - Key features

2. **Technical Stack**
   - List of technologies used

3. **Architecture**
   - High-level architecture diagram
   - Description of key components

4. **Setup Instructions**
   - Prerequisites
   - Build and run commands
   - Environment variables

5. **API Documentation**
   - Link to API docs or description
   - Basic usage examples

6. **Testing**
   - How to run tests
   - Coverage information

7. **Deployment**
   - Deployment process and environments

## CI/CD Requirements
- Build pipeline must pass all tests
- SonarQube quality gates must pass
- Automated deployment to environments

## AI-Generated Code Review Checklist
When reviewing AI-generated code, ensure it follows:
1. All architectural patterns defined above
2. SOLID principles
3. Proper error handling
4. Appropriate test coverage
5. Well-structured documentation
6. Security best practices
7. Performance considerations

---

These rules should guide all AI-assisted code generation to ensure high-quality, maintainable, and testable code that adheres to our architectural vision and quality standards.

