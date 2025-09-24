---
title: "Elixir Phoenix Cursor Rules"
description: "You are an expert in Elixir, Phoenix, PostgreSQL, LiveView, and Tailwind CSS. This document outlines coding style, structure, and best practices for developing applications using these technologies."
category: "rules"
tags: ["Elixir", "Phoenix", "PostgreSQL", "LiveView", "Tailwind CSS"]
tech_stack: ["elixir", "phoenix", "ecto", "live_view", "tailwind", "postgresql"]
---

You are an expert in Elixir, Phoenix, PostgreSQL, LiveView, and Tailwind CSS.

### Code Style and Structure
- Write **concise** and **idiomatic** Elixir code, ensuring clarity with accurate examples.
- Adhere to **Phoenix conventions** and best practices.
- Utilize **functional programming** patterns and embrace **immutability**.
- Favor **higher-order functions** and **recursion** over traditional imperative loops.
- Choose **descriptive names** for variables and functions (e.g., `user_signed_in?`, `calculate_total`).
- Organize files according to **Phoenix conventions** (controllers, contexts, views, etc.).

### Naming Conventions
- Use **snake_case** for file names, function names, and variables.
- Use **PascalCase** for module names.
- Follow **Phoenix naming conventions** for contexts, schemas, and controllers.

### Elixir and Phoenix Usage
- Effectively use **pattern matching** and **guards** in Elixir.
- Leverage built-in functions and macros provided by **Phoenix**.
- Utilize **Ecto** for efficient database operations.

### Syntax and Formatting
- Follow the **Elixir Style Guide** ([link](https://github.com/christopheradams/elixir_style_guide)).
- Use the **pipe operator** (`|>`) for chaining functions.
- Prefer **single quotes** for charlists and **double quotes** for strings.

### Error Handling and Validation
- Embrace Elixir's **"let it crash"** philosophy and utilize **supervisor trees**.
- Implement robust **error logging** and provide user-friendly messages.
- Use **Ecto changesets** for data validation.
- Handle errors gracefully in controllers, displaying appropriate **flash messages**.

### UI and Styling
- Use **Phoenix LiveView** for dynamic, real-time interactions.
- Implement responsive design principles with **Tailwind CSS**.
- Utilize **Phoenix view helpers** and templates to maintain DRY (Don't Repeat Yourself) principles.

### Performance Optimization
- Effectively use **database indexing**.
- Implement caching strategies (e.g., **ETS**, **Redis**).
- Use **Ecto's preload** to prevent N+1 query issues.
- Optimize database queries through **preload**, **joins**, or **select** statements.

### Key Conventions
- Adhere to **RESTful routing conventions**.
- Organize related functionality using **contexts**.
- Implement **GenServers** for stateful processes and background jobs.
- Use **Tasks** for concurrent, isolated jobs.

### Testing
- Write comprehensive tests using **ExUnit**.
- Follow **Test-Driven Development (TDD)** practices.
- Utilize **ExMachina** for generating test data.

### Security
- Implement robust **authentication** and **authorization** (e.g., **Guardian**, **Pow**).
- Use strong parameters in controllers for **params validation**.
- Protect against common web vulnerabilities (e.g., **XSS**, **CSRF**, **SQL injection**).

### Core Principles
- **Domain-Driven Design**: Structure code around business domains rather than technical layers.
- **Functional Core, Imperative Shell**: Keep pure domain logic separate from side effects.
- **Explicit Over Implicit**: Favor clarity over obscurity.
- **Composition Over Inheritance**: Build systems from small, focused components.
- **Single Responsibility**: Ensure each module and function has a single purpose.
- **Easy to Change**: Design for maintainability and adaptability.
- **Fail Fast**: Identify and handle errors as early as possible.
- **YAGNI (You Aren't Gonna Need It)**: Avoid building features until they are necessary.

### Project Structure
- **Context-Based Organization**: Use Phoenix contexts to define domain boundaries.
  ```
  lib/my_app/
    accounts/     # User management domain
    billing/      # Payment processing domain
    catalog/      # Product catalog domain
  ```
- **API/Implementation Separation**: Public API modules should delegate to implementation modules.
  ```elixir
  # In MyApp.Accounts (API module)
  defdelegate create_user(attrs), to: MyApp.Accounts.UserCreator
  ```
- **Boundary Enforcement**: Use tools like **NimbleOptions** to validate inputs at boundaries.

### Coding Patterns
- **Pattern Matching**: Use pattern matching in function heads for control flow.
- **Railway-Oriented Programming**: Chain operations with `with` for elegant error handling.
  ```elixir
  with {:ok, user} <- find_user(id),
       {:ok, updated} <- update_user(user, attrs) do
    {:ok, updated}
  end
  ```
- **Type Specifications**: Add typespecs to all public functions.
  ```elixir
  @spec create_user(user_attrs()) :: {:ok, User.t()} | {:error, Changeset.t()}
  ```
- **Immutable Data Transformations**: Return new state instead of modifying existing state.
- **Data Validation**: Validate data at boundaries using **Ecto.Changeset**, even outside of database contexts.
  ```elixir
  def validate_attrs(attrs) do
    {%{}, %{name: :string, email: :string}}
    |> Ecto.Changeset.cast(attrs, [:name, :email])
    |> Ecto.Changeset.validate_required([:name, :email])
    |> Ecto.Changeset.validate_format(:email, ~r/@/)
  end
  ```
- **Result Tuples**: Return tagged tuples like `{:ok, result}` or `{:error, reason}` for operations that can fail.

### Process Design
- **GenServer for State**: Use **GenServers** for managing stateful processes.
- **Supervision Trees**: Design appropriate supervision hierarchies.
- **Registry Pattern**: Utilize **Registry** for dynamic process lookup.
- **Task.Supervisor**: Use for concurrent operations that may fail.
- **Process Isolation**: Design processes to crash independently without affecting the entire system.
- **Let It Crash**: Embrace the "let it crash" philosophy with proper supervision.

### Phoenix Best Practices
- **LiveView-First**: Prioritize **LiveView** as the primary UI technology.
- **Function Components**: Create reusable UI elements using function components.
- **PubSub for Real-time**: Employ **Phoenix PubSub** for real-time features.
- **Context Boundaries**: Respect context boundaries in controllers and LiveViews.
- **Thin Controllers**: Keep controllers lightweight, delegating business logic to contexts.
- **Security First**: Always consider security implications (e.g., **CSRF**, **XSS**).

### Testing Strategies
- **Test Public APIs**: Focus on testing public context APIs.
- **Mox for Dependencies**: Use **Mox** for mocking external dependencies.
- **Property-Based Testing**: Utilize **StreamData** for property-based tests.
- **Test Factories**: Employ **ExMachina** for creating test data.
- **Test Readability**: Write tests that serve as documentation.
- **Arrange-Act-Assert**: Structure tests with clear setup, action, and verification phases.

### HTTP and API Integration
- **Req for HTTP Clients**: Use **Req** instead of **HTTPoison** or **Tesla**.
- **Behaviours for API Clients**: Define behaviours for API clients to facilitate easy mocking.
- **Error Handling**: Gracefully handle network failures and unexpected responses.
- **Timeouts**: Always set appropriate timeouts for external calls.
- **Circuit Breakers**: Implement circuit breakers for critical external services.

### Documentation and Quality
- **Document Public Functions**: Add `@doc` to all public functions.
- **Examples in Docs**: Include examples in documentation.
- **Credo and Dialyzer**: Utilize these tools for static analysis and type checking.
- **Consistent Formatting**: Use `mix format` to maintain a consistent code style.
- **Continuous Refactoring**: Regularly improve code structure without altering behavior.
- **Comments**: Write comments only when necessary, focusing on why rather than what.

### Performance Considerations
- **Avoid N+1 Queries**: Utilize **Ecto's** preloading and joins.
- **Pagination**: Implement pagination for large result sets.
- **Background Jobs**: Use **Oban** for background processing.
- **Measure First**: Profile code before optimizing.
- **Caching**: Apply strategic caching where appropriate.