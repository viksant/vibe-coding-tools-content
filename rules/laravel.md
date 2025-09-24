---
title: "Comprehensive Laravel PHP Cursor Rules: Best Practices and Key Principles"
description: "You are an expert in Laravel, PHP, and related web development technologies. This document outlines essential principles, standards, and best practices for developing with Laravel and PHP."
category: "rules"
tags: ["Laravel", "PHP", "Best Practices", "Web Development"]
tech_stack: ["laravel", "php", "livewire", "alpinejs", "tailwindcss", "daisyui"]
---

You have a solid foundation in Laravel, PHP, Livewire, Alpine.js, TailwindCSS, and DaisyUI. Let’s break down some core principles and best practices that can help you write cleaner and more maintainable code.

### Core Principles
Start by crafting clear and concise technical responses. Use accurate examples of PHP and Laravel to illustrate your points. It’s essential to prioritize the **SOLID** principles for object-oriented programming. This approach leads to a maintainable architecture.

Stick to PHP and Laravel best practices. This habit ensures your code remains consistent and easy to read. When designing systems, focus on scalability and maintainability so you can accommodate future growth. Embrace iteration and modularization to boost reusability and avoid repeating code. Finally, use descriptive names for variables, methods, and classes. This practice enhances clarity in your code.

### Dependencies
Make sure you have the following dependencies ready to go:
- **Composer** for managing your dependencies
- **PHP 8.3+**
- **Laravel 11.0+**

### PHP and Laravel Standards
Take advantage of PHP 8.3+ features whenever you can, like typed properties and match expressions. Stick to **PSR-12** coding standards to maintain a consistent style across your code. Always declare strict typing with `declare(strict_types=1);` to catch potential issues early.

Leverage Laravel's built-in features and helpers to save time and effort. Keep to Laravel's directory structure and naming conventions for better organization. Implement robust error handling and logging by utilizing Laravel's exception handling and logging features. Create custom exceptions as needed, and remember to use try-catch blocks for expected exceptions.

Use Laravel's validation features to check form and request data, and implement middleware to filter and modify requests. For database interactions, rely on Laravel's **Eloquent ORM** and the query builder for complex operations. Don't forget to create and maintain proper database migrations and seeders.

### Laravel Best Practices
Opt for **Eloquent ORM** and Query Builder instead of raw SQL queries. Use Repository and Service patterns to enhance code organization and reusability. Take advantage of Laravel's built-in authentication and authorization features, such as Sanctum and Policies.

Consider using caching mechanisms like Redis and Memcached to boost performance. For managing long-running tasks and background processing, implement job queues and **Laravel Horizon**. Conduct thorough testing with PHPUnit and Laravel Dusk to cover unit, feature, and browser tests. 

When building APIs, make sure to implement API resources and versioning for better maintainability. Proper error handling and logging are crucial as well, so utilize Laravel's exception handler and logging facade. Use Laravel's validation features, including Form Requests, to ensure data integrity. 

Don't forget to implement database indexing and use Laravel's query optimization features. Tools like **Laravel Telescope** can help you debug and monitor performance during development. For quick admin panel development, consider using **Laravel Nova** or **Filament**. Lastly, make sure to incorporate security measures like CSRF protection, XSS prevention, and input sanitization.

### Code Architecture
Let’s talk about naming conventions. Keep your naming consistent for folders, classes, and files. Follow Laravel's conventions: use singular for models and plural for controllers, like `User.php` for the model and `UsersController.php` for the controller. Use **PascalCase** for class names, **camelCase** for method names, and **snake_case** for database columns.

When it comes to controllers, design them as final classes to prevent inheritance. Keep them read-only, avoiding property mutations. Instead of injecting dependencies directly, consider using method injection or service classes.

For models, also use final classes to maintain data integrity. Create a **Services** folder within the app directory and organize services based on models and other needs. Service classes should be final and read-only, focusing on complex business logic to keep controllers light.

Maintain organized and consistent routes, creating separate route files for major models or features. Group related routes together, like all user-related routes in `routes/user.php`. 

Always use explicit return type declarations for methods and functions, and employ appropriate PHP type hints for parameters. PHP 8.3+ features like union types and nullable types can come in handy as well.

Be explicit and consistent with data type declarations throughout your codebase. Utilize type hints for properties, method parameters, and return types, and enforce strict typing to catch type-related errors early.

For error handling, use Laravel's exception handling and logging features to manage issues. Create custom exceptions when necessary and handle exceptions gracefully, returning appropriate responses.

### Key Points
Follow Laravel’s **MVC architecture** to separate business logic, data, and presentation layers clearly. Implement request validation using **Form Requests** to secure and validate data inputs. Leverage Laravel’s built-in authentication system, including **Laravel Sanctum** for API token management.

Ensure your REST API meets Laravel standards by using API Resources for structured responses. Automate recurring tasks with task scheduling and event listeners, and ensure data consistency by implementing database transactions with Laravel's database facade.

Use **Eloquent ORM** for database interactions, enforcing relationships and optimizing queries. Implement API versioning for better maintainability and backward compatibility. Optimize performance with caching mechanisms like **Redis** and **Memcached**. Finally, ensure robust error handling and logging with Laravel’s exception handler and logging features.