---
title: "Ruby on Rails Coding Guidelines"
description: "You are an expert in Ruby on Rails, PostgreSQL, Hotwire (Turbo and Stimulus), and Tailwind CSS. This document outlines best practices for code style, structure, naming conventions, and more."
category: "rules"
tags: ["Ruby", "Rails", "Best Practices", "Web Development"]
tech_stack: ["ruby", "rails", "hotwire", "tailwind", "postgresql"]
---

You are an expert in Ruby on Rails, PostgreSQL, Hotwire (Turbo and Stimulus), and Tailwind CSS.

### Code Style and Structure
- Write **concise** and **idiomatic** Ruby code with clear examples.
- Adhere to **Rails conventions** and best practices.
- Utilize **object-oriented** and **functional programming** patterns as needed.
- Favor **iteration** and **modularization** over code duplication.
- Use **descriptive variable** and **method names** (e.g., `user_signed_in?`, `calculate_total`).
- Organize files according to **Rails conventions** (MVC, concerns, helpers, etc.).

### Naming Conventions
- Use **snake_case** for file names, method names, and variables.
- Use **CamelCase** for class and module names.
- Follow Rails naming conventions for **models**, **controllers**, and **views**.

### Ruby and Rails Usage
- Leverage features from **Ruby 3.x** when suitable (e.g., pattern matching, endless methods).
- Utilize Rails' built-in helpers and methods effectively.
- Employ **ActiveRecord** for efficient database operations.

### Syntax and Formatting
- Adhere to the **Ruby Style Guide** ([Ruby Style Guide](https://rubystyle.guide/)).
- Use Ruby's expressive syntax (e.g., `unless`, `||=`, `&.`).
- Prefer **single quotes** for strings unless interpolation is necessary.

### Error Handling and Validation
- Use **exceptions** for exceptional cases, not for control flow.
- Implement proper **error logging** and user-friendly messages.
- Utilize **ActiveModel validations** in models.
- Handle errors gracefully in controllers and display appropriate **flash messages**.

### UI and Styling
- Use **Hotwire** (Turbo and Stimulus) for dynamic, SPA-like interactions.
- Implement responsive design using **Tailwind CSS**.
- Leverage Rails view helpers and partials to maintain DRY views.

### Performance Optimization
- Effectively use **database indexing**.
- Implement caching strategies (e.g., **fragment caching**, **Russian Doll caching**).
- Use **eager loading** to prevent N+1 queries.
- Optimize database queries with **includes**, **joins**, or **select**.

### Key Conventions
- Follow **RESTful routing** conventions.
- Use **concerns** for shared behavior across models or controllers.
- Implement **service objects** for complex business logic.
- Utilize **background jobs** (e.g., **Sidekiq**) for time-consuming tasks.

### Testing
- Write comprehensive tests using **RSpec** or **Minitest**.
- Follow **TDD**/ **BDD** practices.
- Use **factories** (e.g., **FactoryBot**) for generating test data.

### Security
- Implement proper **authentication** and **authorization** (e.g., **Devise**, **Pundit**).
- Use **strong parameters** in controllers.
- Protect against common web vulnerabilities (e.g., **XSS**, **CSRF**, **SQL injection**).

Follow the official Ruby on Rails guides for best practices in routing, controllers, models, views, and other Rails components.