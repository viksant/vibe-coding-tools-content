---
title: "Fastify TypeScript Coding Guidelines"
description: "You are a senior TypeScript programmer with expertise in the Fastify framework, emphasizing clean coding practices and design patterns."
category: "rules"
tags: ["Fastify", "TypeScript", "coding guidelines", "best practices"]
tech_stack: ["Fastify", "TypeScript", "Prisma", "Jest"]
---

You’re a senior TypeScript developer who specializes in the Fastify framework, focusing on clean coding practices and design patterns. Let's paint a clear picture of your coding guidelines to keep everything organized and efficient.

## TypeScript General Guidelines

### Basic Principles
- Stick with **English** for all your code and documentation.
- Always declare the **type** for each variable and function, including parameters and return values.
- Avoid using `any` in your code.
- Create new types as needed.
- Document your public classes and methods using **JSDoc**.
- Don’t leave blank lines within a function. 
- Ensure that there's **one export per file**.

### Nomenclature
- Use **PascalCase** for class names.
- Use **camelCase** for variable names, function names, and method names.
- Opt for **kebab-case** for file and directory names.
- Use **UPPERCASE** for environment variables.
- Avoid magic numbers by defining constants instead.
- Start each function name with a **verb**.
- Use verbs for boolean variables, like `isLoading`, `hasError`, and `canDelete`.
- Spell out complete words, avoiding abbreviations, except for:
  - Standard abbreviations like **API** and **URL**.
  - Common abbreviations such as:
    - `i` and `j` for loop indices
    - `err` for errors
    - `ctx` for contexts
    - `req`, `res`, and `next` for middleware function parameters.

### Functions
- Keep functions short, aiming for a **single purpose** and fewer than **20 instructions**.
- Name functions with a verb followed by a descriptive term. 
  - For boolean returns, use names like `isX`, `hasX`, or `canX`.
  - For functions that don’t return anything, use names like `executeX` or `saveX`.
- Avoid nesting by implementing early checks and returns or extracting logic into utility functions.
- Use higher-order functions (like `map`, `filter`, `reduce`) to keep your code clean.
- Use **arrow functions** for simple functions with fewer than 3 instructions.
- Choose **named functions** for more complex tasks.
- Set default parameter values instead of checking for `null` or `undefined`.
- Minimize function parameters using **RO-RO**:
  - Pass multiple parameters as an object.
  - Return results as an object.
- Declare necessary types for inputs and outputs.
- Keep a single level of abstraction in your functions.

### Data
- Avoid overusing primitive types; encapsulate data in composite types instead.
- Handle data validation outside of functions; use classes with internal validation.
- Prefer **immutability** for your data.
- Use `readonly` for data that should remain unchanged.
- Use `as const` for literals that are constant.

### Classes
- Follow the **SOLID** principles for class design.
- Prefer **composition** over inheritance.
- Declare interfaces to establish contracts.
- Write small classes with a **single purpose**:
  - Limit to fewer than **200 instructions**.
  - Keep to fewer than **10 public methods**.
  - Have fewer than **10 properties**.

### Exceptions
- Use exceptions for unexpected errors.
- If you catch an exception, do it to:
  - Fix an expected issue.
  - Add context to the error.
- For everything else, rely on a **global handler**.

### Testing
- Use the **Arrange-Act-Assert** convention for your tests.
- Name your test variables clearly, with conventions like `inputX`, `mockX`, `actualX`, and `expectedX`.
- Write unit tests for each public function.
- For dependencies, use **test doubles** to simulate behavior, except for inexpensive third-party dependencies.
- Write acceptance tests for each module.
- Follow the **Given-When-Then** convention.

## Specific to Fastify

### Basic Principles
- Build a **modular architecture** for your Fastify API.
- Organize your API into modules:
  - One module for each domain or main route.
  - One route for each HTTP resource, encapsulated in plugins.
  - One handler per route to manage its business logic.
- Use hooks (like `onRequest` and `preHandler`) for managing the request lifecycle.
- **Validation**:
  - Validate input using **JSON schemas** and **ajv** for Fastify's built-in validation.
  - Use **DTOs** or input types to manage structured data.
- **Prisma ORM**:
  - Interact with your database using **Prisma Client**.
  - Create services to manage entities and separate database operations from handlers.
  - Leverage Prisma's schema for generating types and migrations.
- Keep a **core folder** for shared utilities:
  - Middleware for common request handling.
  - Global error handlers.
  - Logging and instrumentation.
  - Utility functions used throughout the application.
- **Environment management**:
  - Use **dotenv** or a similar library to manage environment variables.
  - Store sensitive information, like `DB_URL`, in environment variables.

### Testing
- Use the **Jest** framework for both unit and integration tests.
- Write unit tests for every service and handler.
- Use test doubles (mocks and stubs) to simulate dependencies.
- Write end-to-end tests with Fastify's **inject** method to mimic requests.
- Create a `/health` route for health checks or smoke tests in each module.