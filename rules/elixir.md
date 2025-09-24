---
title: "Elixir Phoenix Cursor Rules"
description: "You are an expert in Elixir, Phoenix, PostgreSQL, LiveView, and Tailwind CSS. This document outlines coding style, structure, and best practices for developing applications using these technologies."
category: "rules"
tags: ["Elixir", "Phoenix", "PostgreSQL", "LiveView", "Tailwind CSS"]
tech_stack: ["elixir", "phoenix", "ecto", "live_view", "tailwind", "postgresql"]
---

You have a solid grasp of Elixir, Phoenix, PostgreSQL, LiveView, and Tailwind CSS. Let’s dive into the key aspects of coding in this environment.

### Code Style and Structure
When writing Elixir code, keep it concise and idiomatic. This means clarity is key, so use accurate examples to illustrate your points. Stick to Phoenix conventions and best practices. Embrace functional programming, focusing on immutability. Rely on higher-order functions and recursion instead of traditional loops. Choose descriptive names for your variables and functions, like `user_signed_in?` and `calculate_total`. Organize your files according to Phoenix conventions, which include controllers, contexts, and views.

### Naming Conventions
Be consistent with naming. Use snake_case for file names, function names, and variables. For module names, stick with PascalCase. Following Phoenix naming conventions for contexts, schemas, and controllers will help maintain clarity.

### Elixir and Phoenix Usage
Make the most of Elixir’s features, like pattern matching and guards. Use the built-in functions and macros from Phoenix to streamline your work. For database interactions, lean on Ecto for efficiency.

### Syntax and Formatting
Check out the Elixir Style Guide for best practices ([link](https://github.com/christopheradams/elixir_style_guide)). Use the pipe operator (`|>`) for chaining functions. Remember to use single quotes for charlists and double quotes for strings.

### Error Handling and Validation
Elixir’s "let it crash" philosophy allows you to handle errors effectively. Use supervisor trees to manage processes. Implement solid error logging and craft user-friendly messages. Leverage Ecto changesets for validating data, and ensure your controllers handle errors gracefully, displaying appropriate flash messages.

### UI and Styling
Use Phoenix LiveView for creating dynamic, real-time interactions. Apply responsive design principles with Tailwind CSS. Take advantage of Phoenix view helpers and templates to keep your code DRY.

### Performance Optimization
Optimize your database performance by utilizing indexing and implementing caching strategies, such as ETS and Redis. Prevent N+1 query issues by using Ecto's preload feature, and optimize your queries with preload, joins, or select statements.

### Key Conventions
Stick to RESTful routing conventions. Organize related functionality using contexts. Use GenServers for stateful processes and background jobs, and Tasks for concurrent, isolated operations.

### Testing
Write thorough tests with ExUnit and adopt Test-Driven Development (TDD) practices. ExMachina can help you generate test data efficiently.

### Security
Ensure robust authentication and authorization with tools like Guardian or Pow. Use strong parameters in controllers to validate incoming data. Protect your application from common web vulnerabilities, such as XSS, CSRF, and SQL injection.

### Core Principles
Consider Domain-Driven Design, structuring your code around business domains rather than technical layers. Keep pure domain logic separate from side effects, and prioritize clarity. Build systems from small, focused components, and ensure each module and function has a single purpose. Design for maintainability, adapt easily to changes, identify errors early, and avoid building unneeded features.

### Project Structure
Organize your project based on contexts to define domain boundaries.
```
lib/my_app/
  accounts/     # User management domain
  billing/      # Payment processing domain
  catalog/      # Product catalog domain
```
Separate public API modules from implementation modules. 

### Coding Patterns
Use pattern matching in function heads for control flow. For error handling, consider using railway-oriented programming with the `with` construct. Specify types for all public functions, and ensure your data transformations are immutable.

### Process Design
Use GenServers for managing stateful processes and design appropriate supervision hierarchies. Implement the Registry pattern for dynamic process lookup and use Task.Supervisor for concurrent operations.

### Phoenix Best Practices
Prioritize LiveView as your main UI technology. Create reusable UI components with function components and use Phoenix PubSub for real-time features. Keep controllers thin by delegating business logic to contexts and always consider security implications.

### Testing Strategies
Focus on testing your public context APIs. Use Mox for mocking dependencies, and take advantage of property-based testing with StreamData. Write tests that not only validate functionality but also serve as documentation.

### HTTP and API Integration
Utilize Req for HTTP clients instead of alternatives like HTTPoison or Tesla. Define behaviours for your API clients to make mocking easier and handle errors gracefully. Always set appropriate timeouts for external calls and consider implementing circuit breakers for critical services.

### Documentation and Quality
Document your public functions with `@doc` and include examples in your documentation. Use tools like Credo and Dialyzer for static analysis and type checking. Maintain a consistent code style with `mix format` and regularly refactor your code to improve its structure.

### Performance Considerations
Avoid N+1 query issues by using Ecto’s preloading and joins. Implement pagination for large datasets and consider background jobs with Oban. Profile your code before optimizing and apply caching strategies where needed.