---
title: "Flask Python Cursor Guidelines"
description: "You are an expert in Python, Flask, and scalable API development. This document outlines key principles and best practices for developing robust Flask applications."
category: "rules"
tags: ["Flask", "Python", "API Development", "Best Practices"]
tech_stack: ["Flask", "Flask-RESTful", "Flask-SQLAlchemy", "Flask-Migrate", "Marshmallow", "Flask-JWT-Extended", "Gunicorn", "uWSGI", "pytest"]
---

You’re diving into the world of Python, Flask, and creating APIs that can handle growth. Let’s break down the key principles and guidelines to keep your project on track.

### Key Principles
First, keep your code clean and precise. Write clear, technical responses and provide accurate Python examples. Embrace functional and declarative programming, and limit your class usage to Flask views. 

Next, strive for iteration and modularization. This practice helps you avoid repeating code. When naming your variables, choose descriptive names that include auxiliary verbs, like `is_active` or `has_permission`. For naming directories and files, stick to lowercase with underscores—for instance, `blueprints/user_routes.py`. It’s often best to use named exports for routes and utility functions. 

Also, implement the **Receive an Object, Return an Object (RORO)** pattern whenever suitable.

### Python/Flask
When defining functions, use `def`. Be sure to add type hints for all function signatures when you can. Organize your file structure clearly: start with Flask app initialization, then move to blueprints, models, utilities, and configuration.

Keep your conditionals clean. Avoid unnecessary curly braces, especially in single-line conditionals. For example, write `if condition: do_something()` without braces.

### Error Handling and Validation
Make error handling and validation a priority. Start your functions by addressing potential errors and edge cases. Use early returns for error conditions to keep your code tidy and prevent deep nesting. Place the happy path last in your functions for easier readability. 

Also, skip unnecessary `else` statements and adopt the if-return pattern instead. Use guard clauses to catch invalid states early. Implement robust error logging and friendly error messages. Consider creating custom error types or factories to ensure consistent error handling.

### Dependencies
Make sure to include these key dependencies:
- **Flask**
- **Flask-RESTful** for developing RESTful APIs
- **Flask-SQLAlchemy** for object-relational mapping (ORM)
- **Flask-Migrate** for handling database migrations
- **Marshmallow** for serialization and deserialization
- **Flask-JWT-Extended** for JSON Web Token (JWT) authentication

### Flask-Specific Guidelines
Utilize Flask application factories to enhance modularity and testing. Organizing routes with Flask Blueprints helps maintain a better code structure. Leverage Flask-RESTful to build RESTful APIs through class-based views.

Make custom error handlers for different exception types. Use Flask’s lifecycle decorators—`before_request`, `after_request`, and `teardown_request`—to manage requests effectively. Take advantage of Flask extensions for common functionalities, like Flask-SQLAlchemy and Flask-Migrate. 

Manage different configurations—development, testing, production—using Flask's config object. Implement solid logging practices with Flask's `app.logger`, and handle authentication and authorization with Flask-JWT-Extended.

### Performance Optimization
For better performance, consider using **Flask-Caching** to cache frequently accessed data. Optimize your database queries with techniques like eager loading and indexing. Implement connection pooling for your database connections and ensure proper session management. 

Lastly, utilize background tasks for operations that take longer to complete, such as using Celery with Flask.

### Key Conventions
Here are some conventions to follow:
1. Use Flask's application context and request context correctly.
2. Focus on API performance metrics, including response time, latency, and throughput.
3. Structure your application effectively:
   - Use blueprints for modular organization.
   - Keep a clear separation of concerns between routes, business logic, and data access.
   - Manage configurations through environment variables.

### Database Interaction
For database operations, use **Flask-SQLAlchemy**. Handle database migrations through **Flask-Migrate**. Be diligent about managing SQLAlchemy sessions and ensure they close after use.

### Serialization and Validation
Leverage **Marshmallow** for both object serialization/deserialization and input validation. Create schema classes for each model to maintain consistent serialization.

### Authentication and Authorization
Implement JWT-based authentication with **Flask-JWT-Extended**. Use decorators to protect routes that require authentication.

### Testing
Write unit tests using **pytest**. Use Flask's test client for integration testing, and set up test fixtures to prepare databases and applications.

### API Documentation
For documentation, consider using **Flask-RESTX** or **Flasgger** for Swagger/OpenAPI documentation. Make sure to thoroughly document all endpoints, including request and response schemas.

### Deployment
When it's time to deploy, use **Gunicorn** or **uWSGI** as your WSGI HTTP server. Implement detailed logging and monitoring in your production environment, and manage sensitive information and configurations with environment variables.

For more details on views, blueprints, and extensions, check out the Flask documentation for best practices.