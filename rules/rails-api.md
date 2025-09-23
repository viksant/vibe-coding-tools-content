---
title: "Rails Ruby API Cursor Rules"
description: "You are an expert in Ruby on Rails, PostgreSQL, and building robust APIs. This document outlines essential coding standards and best practices for API development."
category: "rules"
tags: ["Ruby", "Rails", "API", "PostgreSQL", "Best Practices"]
tech_stack: ["rails", "ruby", "OpenAPI", "API", "postgresql", "JWT", "OAuth2", "Pundit", "CanCanCan", "Sidekiq", "GoodJob", "FactoryBot"]
---

You are an expert in Ruby on Rails, PostgreSQL, and building robust APIs. 

### Code Quality & Conventions
- Write **concise** and **idiomatic** Ruby code, adhering to the [Ruby Style Guide](https://rubystyle.guide/).
- Follow Rails conventions for file structure (e.g., `app/controllers/api/v1/`) and naming conventions: use `snake_case` for files, methods, and variables, and `CamelCase` for classes and modules; models should be singular, while controllers and tables should be plural.
- Apply **object-oriented principles**: utilize Service Objects for complex business logic, Query Objects for intricate lookups, and Concerns for shared behavior.
- Maintain the **DRY** (Don't Repeat Yourself) principle.
- Use **descriptive names** for classes, methods, and variables to enhance code readability.
- Take advantage of features introduced in **Ruby 3.x**.
- Utilize Rails' built-in helpers and methods in their designated contexts.

### API Design & Controller Logic
- Use `ActionController::API` as the base class for your API controllers.
- Keep controllers **lean**: focus on authentication/authorization, parameter parsing (using Strong Parameters), invoking business logic (models/services), and rendering responses (via serializers).
- Implement standard **RESTful actions** (index, show, create, update, destroy) with the corresponding HTTP verbs (GET, POST, PUT/PATCH, DELETE).
- Return meaningful **status codes** for successful operations (200 OK, 201 Created, 204 No Content).
- Employ **Strong Parameters** rigorously to whitelist permitted attributes and prevent mass assignment.
- Use namespaced routes for API versioning, e.g., 
  ```ruby
  namespace :api do 
    namespace :v1 do 
      resources :users 
    end 
  end
  ```
- Favor `resources` and `resource` for standard RESTful routes, limiting exposed actions with `only` or `except`.

### Error Handling & Standardized Responses
- **Centralize Exception Handling**: Use `rescue_from` within a shared base API controller (e.g., `Api::BaseController`) that all API controllers inherit from.
- **Map Exceptions to Status Codes**: Define `rescue_from` handlers to translate common application and framework exceptions (e.g., `ActiveRecord::RecordNotFound`, `ActionController::ParameterMissing`) into specific HTTP status codes (404, 422, 400, 403, etc.) and standardized JSON error responses.
- **Standardized Error Format**: Create and consistently use a JSON structure for all error responses, such as an errors array where each object contains fields like `status`, `title`, `detail`, and optionally `source`.
- Ensure comprehensive **logging** for server errors (500s) and significant exceptions handled by `rescue_from`.
- Avoid using exceptions for normal control flow; reserve them for genuinely exceptional conditions.

### Data Management & Business Logic
- Utilize **ActiveRecord** effectively for database interactions, including scopes, associations, and transactions.
- Implement **ActiveModel validations** extensively in models; failed validations during `save!` or `create!` will raise `ActiveRecord::RecordInvalid`, which should be handled by `rescue_from` to return a 422 response.
- Design **Service Objects** to encapsulate complex business processes or workflows, returning results or raising specific, meaningful exceptions that `rescue_from` can map to appropriate responses.
- Use **Query Objects** for complex database lookups to keep controllers and models clean.
- Use model callbacks sparingly, especially for logic involving external systems or complex side effects; prefer explicit calls from Service Objects.

### Serialization & Response Shaping
- Use **serializers** (e.g., Jbuilder, Active Model Serializers, Blueprinter) to define the structure of JSON responses, ensuring that presentation logic is separate from controllers and models.
- Maintain consistency in JSON structure across all endpoints for both success and error responses, with the error structure dictated by the `rescue_from` handlers.

### Security
- Implement robust **token-based authentication** (JWT, OAuth2). Handle authentication failures via exceptions mapped to 401 Unauthorized responses by `rescue_from`.
- Implement **authorization** (e.g., Pundit, CanCanCan). Handle authorization failures via exceptions mapped to 403 Forbidden responses by `rescue_from`.
- Enforce **HTTPS** across the application.
- Carefully configure **CORS** (Cross-Origin Resource Sharing) using `rack-cors` if the API needs to be accessed from different origins.
- Implement **Rate Limiting** (e.g., using `rack-attack`) to prevent abuse.
- Manage secrets securely using Rails encrypted credentials or environment variables.
- Keep all dependencies updated and regularly audit them for security vulnerabilities (e.g., `bundle audit`, `brakeman`).

### Performance
- Actively prevent **N+1 queries** by using eager loading (`includes`, `preload`) when accessing associations that will be serialized. Use tools like **Bullet** in development to detect issues.
- Use **database indexing** effectively on frequently queried columns, foreign keys, and columns used in WHERE clauses.
- Optimize database queries; use `select` for specific columns where appropriate.
- Implement **caching strategies** (response caching with HTTP headers, fragment caching in serializers, low-level caching with `Rails.cache`) where performance gains outweigh complexity.
- Offload any time-consuming or non-essential tasks triggered by API requests (e.g., sending emails, processing images) to background job systems (e.g., **Sidekiq**, **GoodJob**).

### Testing
- Prioritize **request specs** (integration tests) using RSpec or Minitest to test the full request-response cycle.
- Ensure that specific actions or inputs correctly trigger the expected exceptions and that the `rescue_from` handlers generate the correct HTTP status code and standardized JSON error response body. Verify success cases and various error conditions (400, 401, 403, 404, 422, 500).
- Use **factories** (FactoryBot) for efficient and readable test data generation.
- Write unit tests for models (validations, scopes, methods), services, query objects, and serializers in isolation.

### Documentation
- Document the API thoroughly using standards like **OpenAPI** (Swagger). Consider tools like **rswag** to generate documentation from request specs.
- Clearly document all endpoints, parameters, authentication methods, possible status codes (success and error), and the standard error response format, providing clear examples for consumers.