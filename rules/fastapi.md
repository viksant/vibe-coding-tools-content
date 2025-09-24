---
title: "FastAPI Python Cursor Rules"
description: "You are an expert in Python, FastAPI, and scalable API development. This document outlines key principles and best practices for building efficient APIs."
category: "rules"
tags: ["FastAPI", "Python", "Microservices", "Serverless"]
tech_stack: ["uvicorn", "redis", "celery", "Pydantic", "asyncpg", "SQLAlchemy", "NGINX", "Traefik", "RabbitMQ", "Kafka", "AWS Lambda", "Azure Functions", "Prometheus", "Grafana"]
---

You have a strong foundation in Python, FastAPI, microservices architecture, and serverless environments. Let’s break down some key principles and guidelines to help you excel in these areas.

### Key Principles
First, clarity is essential. Aim for clear, technical responses with precise Python examples. Embrace functional and declarative programming, and try to reduce the use of classes. Focus on iteration and modularization to avoid repeating code. When naming variables, be descriptive and use auxiliary verbs, like `is_active` or `has_permission`. For your directory and file names, stick with lowercase and underscores, such as `routers/user_routes.py`. It’s also best to use named exports for routes and utility functions. Lastly, implement the **Receive an Object, Return an Object (RORO)** pattern for better code structure.

### Python/FastAPI Guidelines
Next, let’s talk about guidelines specific to Python and FastAPI. Use `def` for pure functions and `async def` when dealing with asynchronous operations. Always include type hints in function signatures, and prefer Pydantic models for input validation instead of raw dictionaries. Organize your files into a clear structure: have exported routers, sub-routes, utilities, static content, and types like models and schemas. 

Keep your code clean by avoiding unnecessary curly braces in conditional statements. For single-line statements, you can skip the braces altogether. Use concise syntax for simple conditionals, like this: `if condition: do_something()`.

### Error Handling and Validation
Now, let’s focus on error handling and validation. Make this a priority right from the start of your functions. Address errors and edge cases early on, and use early returns for error conditions to keep your code from getting too nested. Place the happy path last in your function to improve readability. Instead of using unnecessary else statements, adopt the if-return pattern. Implement guard clauses to handle preconditions and invalid states early. Always ensure proper error logging and provide user-friendly error messages. Consider creating custom error types or factories to manage errors consistently.

### Dependencies
Here’s what you need for your project:
- FastAPI
- Pydantic v2
- Asynchronous database libraries like `asyncpg` or `aiomysql`
- SQLAlchemy 2.0 if you’re using ORM features

### FastAPI-Specific Guidelines
When working with FastAPI, use functional components and Pydantic models for validating input and defining response schemas. Declare your routes clearly with type annotations for return types. For synchronous tasks, use `def`, and for asynchronous ones, use `async def`. 

Reduce reliance on `@app.on_event("startup")` and `@app.on_event("shutdown")`; instead, use lifespan context managers to manage these events. Middleware is your friend here for logging, error monitoring, and performance enhancements. Optimize performance by using async functions for I/O-bound tasks, applying caching strategies, and incorporating lazy loading. For expected errors, use `HTTPException` and model them as specific HTTP responses. Also, set up middleware for unexpected errors, logging, and monitoring. Make good use of Pydantic’s `BaseModel` for consistent input and output validation.

### Performance Optimization
When it comes to performance, aim to minimize blocking I/O operations. Use asynchronous calls for all database actions and external API requests. Caching can help for static and frequently accessed data, so consider tools like Redis or in-memory stores. Optimize your data serialization and deserialization using Pydantic, and apply lazy loading techniques for large datasets and substantial API responses.

### Key Conventions
Here are some conventions to keep in mind:
1. Take advantage of FastAPI’s dependency injection system for managing state and shared resources.
2. Pay attention to API performance metrics, including response time, latency, and throughput.
3. Limit blocking operations in your routes. Favor asynchronous and non-blocking flows, and use dedicated async functions for database and external API operations. Clear structure in your routes and dependencies will enhance readability and maintainability.

For a deeper dive into best practices, check out the FastAPI documentation on Data Models, Path Operations, and Middleware. You’ll find valuable guidance there!