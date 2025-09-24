---
title: "Rails Ruby API Cursor Rules"
description: "You are an expert in Ruby on Rails, PostgreSQL, and building robust APIs. This document outlines essential coding standards and best practices for API development."
category: "rules"
tags: ["Ruby", "Rails", "API", "PostgreSQL", "Best Practices"]
tech_stack: ["rails", "ruby", "OpenAPI", "API", "postgresql", "JWT", "OAuth2", "Pundit", "CanCanCan", "Sidekiq", "GoodJob", "FactoryBot"]
---

You have a solid foundation in Ruby on Rails, PostgreSQL, and API development. Let’s refine your approach to enhance your coding experience and create efficient applications.

### Code Quality & Conventions
First, focus on writing Ruby code that is clear and idiomatic. Stick to the [Ruby Style Guide](https://rubystyle.guide/) for consistency. Organize your files following Rails conventions, placing them in structures like `app/controllers/api/v1/`. For naming, use `snake_case` for files, methods, and variables while opting for `CamelCase` for classes and modules. Remember, models should be singular, but controllers and tables are plural.

Next, lean into object-oriented principles. Use Service Objects to manage complex logic, Query Objects for detailed lookups, and Concerns to share behaviors across your application. Always keep the DRY principle in mind to avoid repetition. Name your classes, methods, and variables descriptively to improve readability. Take advantage of the features introduced in Ruby 3.x and use Rails' built-in helpers and methods appropriately.

### API Design & Controller Logic
When designing your API, start with `ActionController::API` as the base for your controllers. Keep them streamlined. Focus on authentication, parameter parsing using Strong Parameters, and invoking business logic through models or services. Make sure to render responses through serializers.

Implement standard RESTful actions like index, show, create, update, and destroy, paired with the appropriate HTTP verbs: GET, POST, PUT/PATCH, and DELETE. Return meaningful status codes, such as 200 for OK, 201 for Created, and 204 for No Content. Always use Strong Parameters to whitelist attributes and prevent mass assignment. For versioning, consider namespaced routes like this:

```ruby
namespace :api do 
  namespace :v1 do 
    resources :users 
  end 
end
```

Stick to `resources` and `resource` for your RESTful routes, using `only` or `except` to limit exposed actions.

### Error Handling & Standardized Responses
For error handling, centralize your approach. Use `rescue_from` in a shared base API controller, like `Api::BaseController`, to manage exceptions across your application. Map exceptions to specific status codes, translating common errors like `ActiveRecord::RecordNotFound` to HTTP status codes such as 404 or 422. 

Create a standardized JSON structure for all error responses. Each error object should include fields like `status`, `title`, `detail`, and optionally `source`. Ensure you log server errors (500s) and any significant exceptions handled by `rescue_from`. Only use exceptions for actual errors, not for regular flow control.

### Data Management & Business Logic
When working with data, use ActiveRecord effectively for database interactions, including scopes, associations, and transactions. Apply ActiveModel validations in your models. If validations fail during `save!` or `create!`, handle the `ActiveRecord::RecordInvalid` exception with `rescue_from` to return a 422 response.

Design Service Objects for complex business processes. These should return results or raise relevant exceptions that `rescue_from` can convert into appropriate responses. Use Query Objects for intricate database lookups to keep your controllers and models clean. Be cautious with model callbacks; use them sparingly and prefer explicit calls from Service Objects for actions involving external systems.

### Serialization & Response Shaping
For shaping your responses, use serializers like Jbuilder, Active Model Serializers, or Blueprinter. This keeps your presentation logic separate from controllers and models. Maintain a consistent JSON structure for both successful and error responses, guided by your `rescue_from` handlers.

### Security
Security is essential. Implement token-based authentication methods like JWT or OAuth2. Handle authentication failures with exceptions that map to 401 Unauthorized responses. Use authorization tools like Pundit or CanCanCan, and manage failures similarly with 403 Forbidden responses.

Always enforce HTTPS across your application. Configure CORS using `rack-cors` if your API needs to be accessed from different origins. Set up Rate Limiting using tools like `rack-attack` to prevent abuse. Secure your secrets with Rails encrypted credentials or environment variables. Regularly update your dependencies and audit them for vulnerabilities using tools like `bundle audit` or `brakeman`.

### Performance
To boost performance, prevent N+1 queries by using eager loading with `includes` or `preload` when accessing associations. Tools like Bullet can help you identify issues during development. Use effective database indexing for frequently queried columns and optimize your database queries by selecting specific columns when needed.

Implement caching strategies where the benefits outweigh the complexities. Consider response caching with HTTP headers, fragment caching in serializers, and low-level caching with `Rails.cache`. Offload time-consuming tasks triggered by API requests, like sending emails or processing images, to background job systems such as Sidekiq or GoodJob.

### Testing
For testing, prioritize request specs, which cover the full request-response cycle, using RSpec or Minitest. Make sure specific actions or inputs trigger the right exceptions and that your `rescue_from` handlers produce the expected HTTP status codes and standardized JSON error responses. Validate both success cases and various error conditions like 400, 401, 403, 404, 422, and 500.

Use factories (FactoryBot) for generating test data efficiently. Write unit tests for your models, services, query objects, and serializers individually.

### Documentation
Finally, document your API thoroughly using standards like OpenAPI (Swagger). Tools like rswag can help generate documentation straight from your request specs. Clearly outline all endpoints, parameters, authentication methods, possible status codes, and the standard error response format, along with examples for users.