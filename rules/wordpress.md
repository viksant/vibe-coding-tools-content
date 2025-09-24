---
title: "Comprehensive WordPress PHP Cursor Rules: Best Practices and Key Principles"
description: "You are an expert in WordPress, PHP, and related web development technologies. This document outlines essential coding principles, best practices, and conventions for developing in WordPress."
category: "rules"
tags: ["WordPress", "PHP", "web development", "best practices"]
tech_stack: ["WordPress", "PHP", "Composer"]
---

You have a solid grasp of WordPress, PHP, and related web development tools. Let’s dive into some key principles and practices to keep your code clean, maintainable, and effective.

### Core Principles
First, aim for clarity in your PHP and WordPress examples. Stick to established practices to ensure your code stays consistent and readable. Emphasizing object-oriented programming can help you create more modular code. 

Next, focus on reusability. Avoid duplicating code by iterating and modularizing your functions. Use descriptive names for your functions, variables, and files. For example, follow directory naming conventions like using lowercase with hyphens (e.g., `wp-content/themes/my-theme`). 

Don’t forget to take advantage of WordPress hooks, such as actions and filters, to extend functionality. Clear, descriptive comments can also make your code easier to understand and maintain.

### PHP/WordPress Coding Practices
When coding, take advantage of features from PHP 7.4 and later, like typed properties and arrow functions. Follow the WordPress PHP coding standards throughout your project. 

At the top of your PHP files, enable strict typing with `declare(strict_types=1);`. Whenever possible, leverage core WordPress functions and APIs. Make sure to maintain the theme and plugin directory structure and naming conventions.

Robust error handling is a must. Use WordPress's built-in debug logging with `WP_DEBUG_LOG`, and create custom error handlers if needed. Implement try-catch blocks for managing exceptions. Always trust WordPress’s built-in functions for validating and sanitizing data. 

When handling forms, ensure security by verifying nonces with submissions. For database interactions, rely on WordPress’s `$wpdb` abstraction layer and use `prepare()` statements for dynamic queries to fend off SQL injection. Use the `dbDelta()` function for managing database schema changes.

### Dependencies
Make sure your plugins or themes are compatible with the latest stable version of WordPress. For more complex projects, consider using Composer for dependency management.

### WordPress Best Practices
When customizing themes, use child themes to maintain compatibility with updates. Avoid altering core WordPress files; instead, extend functionality with hooks. Organize your theme-specific functions within `functions.php`.

Utilize WordPress’s user roles and capabilities for managing permissions effectively. The transients API can help with caching data and enhancing performance. For long-running tasks, use `wp_cron()` to handle background processing.

Write unit tests with WordPress’s `WP_UnitTestCase` framework to ensure code reliability. Follow best practices for internationalization by employing WordPress localization functions. Secure your code by verifying nonces, sanitizing inputs, and escaping data where necessary.

Manage scripts and styles efficiently using `wp_enqueue_script()` and `wp_enqueue_style()`. When necessary, use custom post types and taxonomies to extend what WordPress can do. Store configuration data safely with WordPress's options API and implement pagination using functions like `paginate_links()`.

### Key Conventions
1. Stick to WordPress’s plugin API to extend functionality in a modular way.
2. Use WordPress’s template hierarchy when developing themes for added flexibility.
3. Always apply WordPress’s built-in functions for sanitizing and validating data to secure user inputs.
4. Utilize template tags and conditional tags in your themes for handling dynamic content.
5. For custom queries, interact with the database through `$wpdb` or `WP_Query`.
6. Use WordPress’s authentication and authorization features to manage secure access.
7. For AJAX requests, consider using `admin-ajax.php` or the WordPress REST API.
8. Leverage WordPress’s hook system for creating extensible and modular code.
9. When needed, implement database operations using transactional functions.
10. Schedule tasks using the `WP_Cron` API to automate workflows. 

By following these guidelines, you’ll create high-quality, maintainable code that enhances the WordPress experience for yourself and your users.