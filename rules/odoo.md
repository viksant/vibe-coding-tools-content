---
title: "Python & Odoo Cursor Guidelines"
description: "You are an expert in Python, Odoo, and enterprise business application development. This document outlines key principles and best practices for effective Odoo development."
category: "rules"
tags: ["Odoo", "Python", "Enterprise", "ORM", "API"]
tech_stack: ["Python", "Odoo", "PostgreSQL", "XML", "JSON"]
---

You’re diving into the world of Python, Odoo, and enterprise business application development. Let’s explore some essential principles and practices to guide your journey.

## Key Principles
First off, clarity is vital. When you craft your technical responses, include specific Odoo examples in Python, XML, and JSON. This helps everyone understand better. Use Odoo’s built-in ORM and API decorators, along with XML view inheritance, to boost modularity in your projects. Always aim for readability and maintainability by sticking to PEP 8 for Python and following Odoo’s best practices. Remember to choose descriptive names for your models, fields, and functions that align with Odoo's naming conventions. Lastly, structure your module with a clear separation of concerns, organizing it into models, views, controllers, data, and security configurations.

## Odoo/Python Development
Now, let’s get into the nitty-gritty of Odoo and Python development. Start by defining your models by inheriting from `models.Model`, making good use of Odoo’s ORM. Incorporate API decorators like `@api.model`, `@api.multi`, `@api.depends`, and `@api.onchange` to enhance functionality. 

When it comes to UI views, create and customize them in XML for different formats like forms, trees, kanban, calendar, and graphs. Use XML inheritance to extend or modify existing views with elements like `<xpath>` and `<field>`. For web controllers, apply the `@http.route` decorator to set up HTTP endpoints and return JSON responses for your APIs.

Make sure to structure your modules effectively. A well-documented `__manifest__.py` file and a clear directory layout for models, views, controllers, data (XML/CSV), and static assets go a long way. Don’t forget about QWeb for dynamic HTML templating in reports and website pages.

## Error Handling and Validation
Error handling and validation are crucial for a smooth user experience. Use Odoo’s built-in exceptions like `ValidationError` and `UserError` to communicate errors to users clearly. Keep your data intact with model constraints using `@api.constrains` and implement strong validation logic. 

In your business logic and controller operations, employ `try-except` blocks for effective error management. Use Odoo’s logging system to capture debug information and any error details. Writing tests with Odoo’s testing framework helps ensure your module remains reliable and maintainable.

## Dependencies
Next, let’s talk dependencies. Ensure your work is compatible with the target version of Odoo. For database needs, PostgreSQL is the preferred choice for advanced ORM operations. Don’t hesitate to incorporate additional Python libraries like `requests` and `lxml` when necessary, ensuring they integrate well with Odoo.

## Odoo-Specific Guidelines
When working within Odoo, use XML to define UI elements and configuration files, making sure they comply with Odoo’s schema and namespaces. Set up robust Access Control Lists (ACLs) and record rules in XML to manage module access and user permissions effectively.

Enable internationalization by marking translatable strings with `_()` and keeping your translation files organized. Take advantage of automated actions, server actions, and scheduled actions (cron jobs) to handle background processing and workflow automation. When customizing functionalities, use Odoo’s inheritance mechanisms instead of altering core code directly. For JSON APIs, ensure you handle data serialization, input validation, and error management properly to keep your data intact.

## Performance Optimization
To boost performance, optimize your ORM queries by using domain filters, context parameters, and computed fields wisely to reduce the database load. Implement caching for static or infrequently updated data to enhance overall performance. For long-running or resource-heavy tasks, consider offloading them to scheduled actions or asynchronous job queues.

Simplifying your XML view structures can also help. Use inheritance to cut down on redundancy and make UI rendering more efficient.

## Key Conventions
Keep in mind these conventions as you work. Adhere to Odoo’s "Convention Over Configuration" approach to reduce boilerplate code. Always prioritize security by enforcing ACLs, record rules, and data validations at every layer. Maintain a modular project structure by clearly separating models, views, controllers, and business logic. Write comprehensive tests and keep clear documentation for easy module maintenance. Finally, leverage Odoo’s built-in features and extend functionality through inheritance, rather than modifying core functionality.

For more insights and best practices in model design, view customization, controller development, and security considerations, refer to the official Odoo documentation. Happy coding!