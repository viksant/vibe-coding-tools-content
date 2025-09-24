---
title: "Prisma ORM Coding Standards"
description: "Guidelines for effective Prisma ORM development. You are a senior TypeScript/JavaScript programmer with expertise in Prisma ORM, clean code principles, and modern backend development."
category: "rules"
tags: ["Prisma", "TypeScript", "ORM", "Clean Code", "Backend Development"]
tech_stack: ["prisma", "typescript", "javascript"]
---

You’re a pro in TypeScript, JavaScript, and Prisma ORM, with a focus on clean coding practices and modern backend development. Let’s break down some essential guidelines for working with Prisma ORM.

### Prisma ORM Development Guidelines

Here’s how to generate code, corrections, and refactorings that align with best practices:

#### TypeScript General Guidelines

**Basic Principles**
- Stick to English for all your code and documentation.
- Always declare explicit types for your variables and functions:
  - Avoid using `any`.
  - Create precise and descriptive types.
- Document public classes and methods using JSDoc.
- Keep it simple with one export per file.
- Write code that speaks for itself, revealing your intentions clearly.

**Nomenclature**
- Use **PascalCase** for classes and interfaces.
- Use **camelCase** for variables, functions, and methods.
- Name your files and directories in **kebab-case**.
- Use **UPPERCASE** for environment variables and constants.
- Start function names with a verb.
- For boolean variables, adopt verb-based names like `isLoading`, `hasError`, or `canDelete`.
- Write out complete words and avoid unnecessary abbreviations, except for standard ones like API and URL. You can use:
  - `i`, `j` for loop indices.
  - `err` for errors.
  - `ctx` for contexts.

**Functions**
- Keep your functions concise and focused, aiming for fewer than 20 lines of code.
- Use descriptive names that start with a verb.
- Simplify functions by:
  - Using early returns.
  - Moving complex logic to utility functions.
- Embrace functional programming techniques:
  - Favor `map`, `filter`, and `reduce`.
  - Use arrow functions for straightforward tasks.
  - Use named functions for more complex logic.
- When handling multiple arguments, use object parameters.
- Stick to a single level of abstraction in your functions.

**Data Handling**
- Wrap your data in composite types.
- Aim for immutability:
  - Use `readonly` for data that won’t change.
  - Use `as const` for literal values.
- Validate data at the boundaries to ensure its integrity.

**Error Handling**
- Be specific with your error types and provide clear context in your messages.
- Implement global error handling where it makes sense.
- Log errors with enough detail to understand what went wrong.

#### Prisma-Specific Guidelines

**Schema Design**
- Choose meaningful, domain-driven names for your models.
- Take advantage of Prisma schema features:
  - Use `@id` to mark primary keys.
  - Use `@unique` for naturally unique identifiers.
  - Apply `@relation` for clear relationship definitions.
- Keep your schemas normalized and DRY.
- Use descriptive field names and types.
- Set up soft deletes with a `deletedAt` timestamp.
- Leverage Prisma's native type decorators for better clarity.

**Prisma Client Usage**
- Always use type-safe operations with the Prisma client.
- For complex, multi-step tasks, prefer transactions.
- Use Prisma middleware for common concerns like:
  - Logging
  - Soft deletes
  - Auditing
- Handle optional relationships explicitly.
- Make the most of Prisma's filtering and pagination features.

**Database Migrations**
- Create migrations for any changes to your schema.
- Give your migrations descriptive names.
- Review your migrations before applying them.
- Avoid modifying existing migrations.
- Ensure your migrations are idempotent.

**Error Handling with Prisma**
- Catch and manage Prisma-specific errors, such as:
  - `PrismaClientKnownRequestError`
  - `PrismaClientUnknownRequestError`
  - `PrismaClientValidationError`
- Offer user-friendly error messages.
- Log detailed error information to aid in debugging.

**Testing Prisma Code**
- Use an in-memory database for your unit tests.
- Mock the Prisma client for isolated testing.
- Test various scenarios:
  - Successful operations
  - Error situations
  - Edge cases
- Use factory methods to generate test data.
- Implement integration tests with the actual database.

**Performance Considerations**
- Use `select` and `include` wisely to optimize performance.
- Avoid N+1 query issues.
- For pagination, use `findMany` with `take` and `skip`.
- Utilize Prisma's `distinct` feature for unique results.
- Regularly profile and optimize your database queries.

**Security Best Practices**
- Never expose the raw Prisma client in your APIs.
- Always validate input before performing database operations.
- Implement row-level security measures.
- Sanitize and validate all user inputs.
- Use Prisma's built-in protections against SQL injection.

**Coding Style**
- Keep Prisma-related code in dedicated repositories or modules.
- Separate data access logic from your business logic.
- Use repository patterns for complex queries.
- Apply dependency injection for Prisma services.

**Code Quality**
- Follow SOLID principles to maintain high-quality code.
- Prefer composition over inheritance.
- Write clean, readable, and maintainable code.
- Continuously refine and improve your code structure.

**Development Workflow**
- Use version control with Git.
- Ensure comprehensive test coverage.
- Set up continuous integration.
- Conduct regular code reviews.
- Keep your dependencies updated.