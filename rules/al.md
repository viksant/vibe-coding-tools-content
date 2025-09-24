---
title: "AL Microsoft Business Central Development Cursor Guidelines"
description: "You are an expert in AL and Microsoft Business Central development."
category: "rules"
tags: ["AL", "Business Central", "Development", "Best Practices"]
tech_stack: ["AL", "Microsoft Business Central", "Visual Studio Code"]
---

You have a strong background in AL and Microsoft Business Central development. Let’s dive into some key principles and guidelines to help you get the most out of your work.

## Key Principles

First, aim for clarity in your responses. Include precise AL code examples to illustrate your points. Use Business Central’s built-in features and tools to fully utilize its capabilities. 

Next, focus on readability and maintainability. Stick to AL coding conventions and best practices specific to Business Central. Use descriptive names for your variables and functions. For example, follow **PascalCase** for public members and **camelCase** for private ones. Organizing your project modularly will help you leverage Business Central's object-based architecture for better reusability and separation of concerns.

## AL/Business Central Guidelines

When defining data structures, use **table objects** and create user interfaces with **page objects**. Make the most of Business Central’s built-in functions for data manipulation and business logic.

The AL language is key for implementing your business rules and data operations. Use **codeunits** to encapsulate and structure your business logic effectively. Keep in mind the object-oriented programming paradigm in AL to maintain clear separation of concerns and modularity. You should also implement AL's trigger system to respond to events and user actions.

## Error Handling and Debugging

For error handling, use **try-catch** blocks, especially when dealing with database operations and external service calls. Communicate effectively with users by reporting errors using the **Error**, **Message**, and **Confirm** functions. 

Take advantage of Business Central's debugger to spot and fix issues. Creating custom error messages can greatly enhance both development and user experience. Also, leverage AL's assertion system to catch logical errors during your development process.

## Dependencies

Make sure you have the following tools and resources:

- **Microsoft Dynamics 365 Business Central**
- **Visual Studio Code** with the AL Language extension
- **AppSource** apps, if needed for specific functionalities
- Carefully vetted **third-party extensions** for compatibility and performance

## Business Central-Specific Guidelines

When modifying existing functionality, use **table extensions** and **page extensions**. To adjust reports, rely on **report extensions**. Centralize your business logic in **codeunits** and use Visual Studio Code for object development and setup.

Utilize Business Central's report objects for data analysis and document generation. Manage user security with permission sets and user groups. Don't forget to use Business Central's built-in testing framework for both unit and integration testing. For data migration between versions, implement data upgrade **codeunits**. Also, consider using **dimensions** for flexible data analysis and reporting.

## Performance Optimization

To improve your database queries, apply appropriate filters and set up table relations. For long-running operations, implement background tasks using **job queue entries**. You can also use AL's **FlowFields** and **FlowFilters** for calculated fields to enhance performance. Finally, optimize your report performance by carefully selecting data items and filters.

## Key Conventions

1. Stick to Business Central's object-based architecture to create modular and reusable application components.
2. Focus on performance optimization and database management throughout your development process.
3. Keep a clear and logical project structure to enhance readability and make object management easier.

For the latest information on AL programming for Business Central, always refer to the official Microsoft documentation: [Microsoft AL Programming Documentation](https://learn.microsoft.com/ja-jp/dynamics365/business-central/dev-itpro/developer/devenv-programming-in-al).