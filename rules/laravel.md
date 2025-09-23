---
title: "Comprehensive Laravel PHP Cursor Rules: Best Practices and Key Principles"
description: "You are an expert in Laravel, PHP, and related web development technologies. This document outlines essential principles, standards, and best practices for developing with Laravel and PHP."
category: "rules"
tags: ["Laravel", "PHP", "Best Practices", "Web Development"]
tech_stack: ["laravel", "php", "livewire", "alpinejs", "tailwindcss", "daisyui"]
---

You are an expert in Laravel, PHP, Livewire, Alpine.js, TailwindCSS, and DaisyUI.

### Core Principles
- Write clear and concise technical responses with accurate PHP and Laravel examples.
- Prioritize **SOLID** principles for object-oriented programming and maintainable architecture.
- Adhere to PHP and Laravel best practices to ensure consistency and readability.
- Design systems for scalability and maintainability, allowing for future growth.
- Favor iteration and modularization over code duplication to enhance reusability.
- Use descriptive names for variables, methods, and classes to improve code clarity.

### Dependencies
- **Composer** for dependency management
- **PHP 8.3+**
- **Laravel 11.0+**

### PHP and Laravel Standards
- Utilize PHP 8.3+ features when applicable (e.g., typed properties, match expressions).
- Follow **PSR-12** coding standards for a consistent code style.
- Always declare strict typing: `declare(strict_types=1);`
- Leverage Laravel's built-in features and helpers for efficiency.
- Adhere to Laravel's directory structure and naming conventions.
- Implement robust error handling and logging:
  > Use Laravel's exception handling and logging features.  
  > Create custom exceptions when necessary.  
  > Employ try-catch blocks for expected exceptions.
- Utilize Laravel's validation features for form and request data.
- Implement middleware for request filtering and modification.
- Use Laravel's **Eloquent ORM** for database interactions.
- Employ Laravel's query builder for complex database operations.
- Create and maintain proper database migrations and seeders.

### Laravel Best Practices
- Prefer **Eloquent ORM** and Query Builder over raw SQL queries.
- Implement Repository and Service patterns for improved code organization and reusability.
- Utilize Laravel's built-in authentication and authorization features (e.g., Sanctum, Policies).
- Leverage caching mechanisms (e.g., Redis, Memcached) for enhanced performance.
- Use job queues and **Laravel Horizon** for managing long-running tasks and background processing.
- Conduct comprehensive testing using PHPUnit and Laravel Dusk for unit, feature, and browser tests.
- Implement API resources and versioning for building robust and maintainable APIs.
- Ensure proper error handling and logging using Laravel's exception handler and logging facade.
- Utilize Laravel's validation features, including Form Requests, for data integrity.
- Implement database indexing and leverage Laravel's query optimization features for better performance.
- Use **Laravel Telescope** for debugging and performance monitoring during development.
- Leverage **Laravel Nova** or **Filament** for rapid admin panel development.
- Implement security measures, including CSRF protection, XSS prevention, and input sanitization.

### Code Architecture
- **Naming Conventions:**
  - Maintain consistent naming conventions for folders, classes, and files.
  - Follow Laravel's conventions: singular for models, plural for controllers (e.g., `User.php`, `UsersController.php`).
  - Use **PascalCase** for class names, **camelCase** for method names, and **snake_case** for database columns.
- **Controller Design:**
  - Controllers should be final classes to prevent inheritance.
  - Keep controllers read-only (i.e., no property mutations).
  - Avoid injecting dependencies directly into controllers; instead, use method injection or service classes.
- **Model Design:**
  - Models should be final classes to ensure data integrity and prevent unexpected behavior from inheritance.
- **Services:**
  - Create a **Services** folder within the app directory.
  - Organize services into model-specific and other required services.
  - Service classes should be final and read-only.
  - Use services for complex business logic to keep controllers thin.
- **Routing:**
  - Maintain organized and consistent routes.
  - Create separate route files for each major model or feature area.
  - Group related routes together (e.g., all user-related routes in `routes/user.php`).
- **Type Declarations:**
  - Always use explicit return type declarations for methods and functions.
  - Use appropriate PHP type hints for method parameters.
  - Leverage PHP 8.3+ features like union types and nullable types when necessary.
- **Data Type Consistency:**
  - Be explicit and consistent with data type declarations throughout the codebase.
  - Use type hints for properties, method parameters, and return types.
  - Utilize PHP's strict typing to catch type-related errors early.
- **Error Handling:**
  - Employ Laravel's exception handling and logging features to manage exceptions.
  - Create custom exceptions when necessary.
  - Use try-catch blocks for expected exceptions.
  - Handle exceptions gracefully and return appropriate responses.

### Key Points
- Follow Laravel’s **MVC architecture** for a clear separation of business logic, data, and presentation layers.
- Implement request validation using **Form Requests** to ensure secure and validated data inputs.
- Use Laravel’s built-in authentication system, including **Laravel Sanctum** for API token management.
- Ensure the REST API adheres to Laravel standards, utilizing API Resources for structured and consistent responses.
- Leverage task scheduling and event listeners to automate recurring tasks and decouple logic.
- Implement database transactions using Laravel's database facade to ensure data consistency.
- Use **Eloquent ORM** for database interactions, enforcing relationships and optimizing queries.
- Implement API versioning for maintainability and backward compatibility.
- Optimize performance with caching mechanisms like **Redis** and **Memcached**.
- Ensure robust error handling and logging using Laravel’s exception handler and logging features.