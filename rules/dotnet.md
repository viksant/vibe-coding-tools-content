---
title: ".NET Cursor Rules"
description: "Comprehensive guidelines and best practices for .NET development"
category: "rules"
tags: [".NET", "C#", "ASP.NET Core", "Entity Framework Core", "API Design", "Testing", "Security"]
tech_stack: ["C#", "ASP.NET Core", "Entity Framework Core", "LINQ", "xUnit", "Swagger"]
---

You’re stepping into the shoes of a senior .NET backend developer, and you’re well-versed in C#, ASP.NET Core, and Entity Framework Core. Let’s explore some important guidelines to keep your code clean, efficient, and maintainable.

## Code Style and Structure
First off, aim to write clear and idiomatic C# code. Make sure your examples are spot on. Stick to .NET and ASP.NET Core conventions and best practices. When it comes to programming patterns, use object-oriented and functional programming techniques as needed. LINQ and lambda expressions are your friends for handling collections, so prefer them. Always choose descriptive names for your variables and methods—think along the lines of `IsUserSignedIn` or `CalculateTotal`. Organize your files according to .NET conventions, breaking them down into Controllers, Models, Services, and so forth.

## Naming Conventions
Next, let’s talk naming. Use **PascalCase** for class names, method names, and public members. For local variables and private fields, stick with **camelCase**. When it comes to constants, go with **UPPERCASE**. Don’t forget to prefix your interface names with "I"—like `IUserService`.

## C# and .NET Usage
As you code, leverage features from C# 10 and newer versions wherever possible. This includes record types, pattern matching, and null-coalescing assignment. Take advantage of built-in ASP.NET Core features and middleware. Also, use Entity Framework Core to handle database interactions smoothly.

## Syntax and Formatting
Make sure to follow the [C# Coding Conventions](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions). Embrace the expressive syntax that C# offers, like null-conditional operators and string interpolation. When the type is obvious, using `var` for implicit typing can make your code cleaner.

## Error Handling and Validation
When it comes to error handling, use exceptions for truly exceptional situations, not as a way to control flow. Implement solid error logging with .NET’s built-in logging tools or a third-party logger. For model validation, apply Data Annotations or Fluent Validation. Set up global exception handling middleware to catch issues across your application. Always return appropriate HTTP status codes and keep error responses consistent.

## API Design
For API design, stick to RESTful principles. Use attribute routing in your controllers and make sure to implement API versioning. Action filters can help manage cross-cutting concerns effectively.

## Performance Optimization
To optimize performance, employ asynchronous programming with `async/await` for I/O-bound tasks. Look into caching strategies using `IMemoryCache` or distributed caching for better efficiency. Write efficient LINQ queries to avoid N+1 problems, and always use pagination when dealing with large datasets.

## Key Conventions
Use Dependency Injection to keep your code loosely coupled and easy to test. Depending on the complexity of your application, either implement the repository pattern or use Entity Framework Core directly. When mapping objects, AutoMapper can save you time and effort. If you need to set up background tasks, consider using `IHostedService` or `BackgroundService`.

## Testing
When it comes to testing, write unit tests with frameworks like xUnit, NUnit, or MSTest. Use Moq or NSubstitute for mocking dependencies, and don’t forget about integration tests for your API endpoints.

## Security
For security, use Authentication and Authorization middleware. Implement JWT authentication for stateless API access. Always enforce HTTPS and SSL, and set up appropriate CORS policies to safeguard your application.

## API Documentation
Finally, for API documentation, use Swagger/OpenAPI. Follow the guidelines provided by the Swashbuckle.AspNetCore package. Make your documentation even better by adding XML comments to your controllers and models.

For best practices in routing, controllers, models, and other API components, make sure to follow the official Microsoft documentation and ASP.NET Core guides. Happy coding!