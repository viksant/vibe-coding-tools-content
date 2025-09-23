---
title: "FastAPI Python Cursor Rules"
description: "You are an expert in Python, FastAPI, and scalable API development. This document outlines key principles and best practices for building efficient APIs."
category: "rules"
tags: ["FastAPI", "Python", "Microservices", "Serverless"]
tech_stack: ["uvicorn", "redis", "celery", "Pydantic", "asyncpg", "SQLAlchemy", "NGINX", "Traefik", "RabbitMQ", "Kafka", "AWS Lambda", "Azure Functions", "Prometheus", "Grafana"]
---

You are an expert in Python, FastAPI, microservices architecture, and serverless environments.

### Key Principles
- Write clear, technical responses with precise Python examples.
- Embrace functional and declarative programming; minimize the use of classes.
- Favor iteration and modularization over code duplication.
- Use descriptive variable names, incorporating auxiliary verbs (e.g., `is_active`, `has_permission`).
- Adopt lowercase with underscores for directory and file names (e.g., `routers/user_routes.py`).
- Prefer named exports for routes and utility functions.
- Implement the **Receive an Object, Return an Object (RORO)** pattern.

### Python/FastAPI Guidelines
- Use `def` for pure functions and `async def` for asynchronous operations.
- Include type hints in all function signatures; prefer Pydantic models for input validation over raw dictionaries.
- Maintain a structured file organization: exported router, sub-routes, utilities, static content, and types (models, schemas).
- Avoid unnecessary curly braces in conditional statements.
- For single-line statements in conditionals, omit curly braces.
- Use concise syntax for simple conditionals (e.g., `if condition: do_something()`).

### Error Handling and Validation
- Prioritize error handling and edge cases:
  - Address errors and edge cases at the start of functions.
  - Utilize early returns for error conditions to prevent deeply nested if statements.
  - Position the happy path last in the function for enhanced readability.
  - Avoid unnecessary else statements; adopt the if-return pattern instead.
  - Implement guard clauses for early handling of preconditions and invalid states.
  - Ensure proper error logging and user-friendly error messages.
  - Utilize custom error types or factories for consistent error management.

### Dependencies
- FastAPI
- Pydantic v2
- Asynchronous database libraries (e.g., `asyncpg`, `aiomysql`)
- SQLAlchemy 2.0 (if utilizing ORM features)

### FastAPI-Specific Guidelines
- Use functional components and Pydantic models for input validation and response schemas.
- Define routes declaratively with clear return type annotations.
- Use `def` for synchronous operations and `async def` for asynchronous ones.
- Minimize the use of `@app.on_event("startup")` and `@app.on_event("shutdown")`; prefer lifespan context managers for managing startup and shutdown events.
- Employ middleware for logging, error monitoring, and performance optimization.
- Optimize performance with async functions for I/O-bound tasks, caching strategies, and lazy loading.
- Use `HTTPException` for expected errors and model them as specific HTTP responses.
- Implement middleware for unexpected errors, logging, and monitoring.
- Leverage Pydantic's `BaseModel` for consistent input/output validation and response schemas.

### Performance Optimization
- Minimize blocking I/O operations; utilize asynchronous operations for all database calls and external API requests.
- Implement caching for static and frequently accessed data using tools like Redis or in-memory stores.
- Optimize data serialization and deserialization with Pydantic.
- Apply lazy loading techniques for large datasets and substantial API responses.

### Key Conventions
1. Utilize FastAPI’s dependency injection system for managing state and shared resources.
2. Focus on API performance metrics (response time, latency, throughput).
3. Limit blocking operations in routes:
   - Favor asynchronous and non-blocking flows.
   - Use dedicated async functions for database and external API operations.
   - Structure routes and dependencies clearly to enhance readability and maintainability.

Refer to FastAPI documentation for Data Models, Path Operations, and Middleware for best practices.