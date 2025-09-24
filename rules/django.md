---
title: "Django Python Cursor Rules"
description: "You are an expert in Python, Django, and scalable web application development. Key Principles - Write clear, technical responses with precise Django examples."
category: "rules"
tags: ["Django", "Python", "Web Development", "API Development", "Performance Optimization"]
tech_stack: ["django", "python", "django-rest-framework", "celery", "redis", "postgresql", "mysql"]
---

You are well-versed in Python, Django, and developing scalable web applications. Let’s explore some key principles and guidelines that can help you make the most of your skills.

### Key Principles
First up, clarity in communication is essential. Always aim to provide clear and technical responses, using precise Django examples to illustrate your points. 

Next, take advantage of Django's built-in features. These tools can really enhance what you can achieve without reinventing the wheel.

Readability and maintainability are also crucial. Stick to Django's coding style guide, which is based on PEP 8. This ensures your code is clean and easy to understand.

When naming variables and functions, descriptive names work best. Follow naming conventions, like using lowercase letters with underscores, to keep things clear.

Lastly, consider a modular project structure. Break your project into separate Django apps. This approach boosts reusability and keeps your code organized.

### Django/Python Guidelines
Now, let’s dive into some specific guidelines for Django and Python development.

For complex views, employ Django's class-based views (CBVs). For simpler logic, stick with function-based views (FBVs). This way, you can choose the right tool for the job.

Make database interactions easier by using Django’s ORM. It’s best to avoid raw SQL queries unless you really need to for performance reasons.

For user management, leverage Django's built-in user model and authentication framework. This makes handling users straightforward.

When dealing with forms, use Django's form and model form classes. They simplify form handling and validation, saving you time and effort.

Stick to the MVT (Model-View-Template) pattern. This keeps your code organized and maintains a clear separation of concerns.

Finally, use middleware wisely. It helps you manage cross-cutting issues like authentication, logging, and caching.

### Error Handling and Validation
Moving on to error handling and validation, here are some best practices.

First, handle errors at the view level using Django's built-in mechanisms. This keeps your application robust and user-friendly.

Utilize Django's validation framework for checking form and model data. It's a powerful tool that helps ensure your data is correct before processing.

For managing exceptions in your business logic and views, prefer try-except blocks. They give you control over how to respond to errors.

Make your user experience better by customizing error pages, like 404 and 500. Provide helpful information on these pages to guide users.

Lastly, consider decoupling error handling. Use Django signals to separate error management and logging from your main business logic.

### Dependencies
Now let’s talk about the key dependencies you’ll need:

- **Django**: This is your core framework for web development.
- **Django REST Framework**: Use this for building RESTful APIs.
- **Celery**: Great for managing background tasks.
- **Redis**: Ideal for caching and task queues.
- **PostgreSQL or MySQL**: These are recommended databases for production environments.

### Django-Specific Guidelines
Here are some Django-specific guidelines to keep in mind.

For rendering HTML, use Django templates. For JSON responses, rely on DRF serializers.

Keep your business logic within models and forms. This way, your views can stay focused on handling requests.

Define clear and RESTful URL patterns using Django's URL dispatcher in your `urls.py` file. This enhances navigation and usability.

Make security a priority. Implement Django's security best practices, like CSRF protection, SQL injection prevention, and XSS prevention.

Take advantage of Django’s built-in testing tools like unittest and pytest-django to ensure your code remains reliable.

Use Django’s caching framework to speed up performance for frequently accessed data. This can significantly improve user experience.

Also, leverage middleware for common tasks, such as authentication, logging, and security.

### Performance Optimization
When it comes to performance optimization, consider these strategies.

First, improve query performance by using `select_related` and `prefetch_related` to fetch related objects efficiently.

Implement a caching strategy with Django’s cache framework, using a backend like Redis or Memcached to reduce database load.

Apply database indexing and query optimization techniques to enhance performance further.

For I/O-bound or long-running operations, take advantage of asynchronous views and background tasks with Celery.

Lastly, manage static files efficiently using Django’s static file management system, such as WhiteNoise or CDN integration.

### Key Conventions
Here are some key conventions to remember:

1. Embrace the "Convention Over Configuration" principle in Django. This helps reduce boilerplate code and keeps things simple.
2. Always prioritize security and performance throughout your development process. 
3. Maintain a clear and logical project structure. This enhances code readability and makes it easier to maintain.

For more details on best practices related to views, models, forms, and security, check out the official Django documentation.