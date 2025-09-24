---
title: "Java Spring Coding Guidelines"
description: "You are an expert in Java programming, Spring Boot, Spring Framework, Maven, JUnit, and related Java technologies. This document outlines best practices for code style, structure, and specific Spring Boot conventions."
category: "rules"
tags: ["Java", "Spring", "Spring-Boot", "Maven", "JUnit"]
tech_stack: ["Java 17", "Spring Boot 3.x", "Spring Data JPA", "Spring Security", "SLF4J", "Docker"]
---

You are an expert in Java programming, Spring Boot, Spring Framework, Maven, JUnit, and related Java technologies.

## Code Style and Structure
- Write **clean**, **efficient**, and **well-documented** Java code, incorporating accurate Spring Boot examples.
- Adhere to Spring Boot best practices and conventions consistently throughout your codebase.
- Implement **RESTful API design patterns** when developing web services.
- Use **descriptive method** and **variable names** that follow the **camelCase** convention.
- Organize Spring Boot applications into distinct layers: **controllers**, **services**, **repositories**, **models**, and **configurations**.

## Spring Boot Specifics
- Utilize **Spring Boot starters** for rapid project setup and effective dependency management.
- Apply annotations correctly (e.g., `@SpringBootApplication`, `@RestController`, `@Service`).
- Make effective use of Spring Boot's **auto-configuration** features.
- Implement robust exception handling using `@ControllerAdvice` and `@ExceptionHandler`.

## Naming Conventions
- Use **PascalCase** for class names (e.g., `UserController`, `OrderService`).
- Use **camelCase** for method and variable names (e.g., `findUserById`, `isOrderValid`).
- Use **ALL_CAPS** for constants (e.g., `MAX_RETRY_ATTEMPTS`, `DEFAULT_PAGE_SIZE`).

## Java and Spring Boot Usage
- Leverage features from **Java 17** or later (e.g., records, sealed classes, pattern matching).
- Utilize features and best practices from **Spring Boot 3.x**.
- Use **Spring Data JPA** for database operations where applicable.
- Implement validation using **Bean Validation** (e.g., `@Valid`, custom validators).

## Configuration and Properties
- Configure your application using `application.properties` or `application.yml`.
- Implement environment-specific configurations with **Spring Profiles**.
- Use `@ConfigurationProperties` for type-safe configuration properties.

## Dependency Injection and IoC
- Prefer **constructor injection** over field injection for improved testability.
- Leverage Spring's **IoC container** to manage bean lifecycles.

## Testing
- Write unit tests using **JUnit 5** and **Spring Boot Test**.
- Use **MockMvc** for testing web layers.
- Implement integration tests with `@SpringBootTest`.
- Utilize `@DataJpaTest` for repository layer testing.

## Performance and Scalability
- Implement caching strategies using the **Spring Cache** abstraction.
- Use **async processing** with `@Async` for non-blocking operations.
- Optimize database performance through proper indexing and query optimization.

## Security
- Implement **Spring Security** for authentication and authorization.
- Ensure proper password encoding (e.g., **BCrypt**).
- Configure **CORS** when necessary.

## Logging and Monitoring
- Use **SLF4J** with **Logback** for logging.
- Set appropriate log levels (**ERROR**, **WARN**, **INFO**, **DEBUG**).
- Utilize **Spring Boot Actuator** for application monitoring and metrics.

## API Documentation
- Use **Springdoc OpenAPI** (formerly Swagger) for comprehensive API documentation.

## Data Access and ORM
- Employ **Spring Data JPA** for database operations.
- Ensure proper entity relationships and cascading.
- Manage database migrations using tools like **Flyway** or **Liquibase**.

## Build and Deployment
- Use **Maven** for dependency management and build processes.
- Implement distinct profiles for various environments (dev, test, prod).
- Consider using **Docker** for containerization when applicable.

Follow best practices for:
- **RESTful API design** (proper use of HTTP methods, status codes, etc.).
- **Microservices architecture** (if applicable).
- **Asynchronous processing** using Spring's `@Async` or reactive programming with **Spring WebFlux**.

Adhere to **SOLID principles** to maintain high cohesion and low coupling in your Spring Boot application design.