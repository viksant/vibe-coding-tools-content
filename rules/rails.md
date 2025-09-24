---
title: "Ruby on Rails Coding Guidelines"
description: "You are an expert in Ruby on Rails, PostgreSQL, Hotwire (Turbo and Stimulus), and Tailwind CSS. This document outlines best practices for code style, structure, naming conventions, and more."
category: "rules"
tags: ["Ruby", "Rails", "Best Practices", "Web Development"]
tech_stack: ["ruby", "rails", "hotwire", "tailwind", "postgresql"]
---

You know your way around Ruby on Rails, PostgreSQL, Hotwire (Turbo and Stimulus), and Tailwind CSS. Let’s break down some key principles to keep your code clean and effective.

### Code Style and Structure
First up, let’s talk about writing code. Aim for concise and idiomatic Ruby that’s easy to understand. Stick to Rails conventions and best practices to keep your projects organized. Embrace both object-oriented and functional programming patterns when it makes sense. Instead of repeating code, think about how you can iterate and modularize your work. Descriptive variable and method names are your friends—use names like `user_signed_in?` or `calculate_total` to make your intentions clear. Don’t forget to organize your files according to Rails conventions, like MVC, concerns, and helpers.

### Naming Conventions
Next, let’s cover naming conventions. Use snake_case for file names, method names, and variables, while class and module names should follow CamelCase. Stick to Rails naming conventions for models, controllers, and views to maintain consistency.

### Ruby and Rails Usage
When using Ruby, take advantage of features from Ruby 3.x, such as pattern matching and endless methods. Rails offers built-in helpers and methods that can streamline your work, so make sure to leverage those. Also, rely on ActiveRecord for your database operations to keep things efficient.

### Syntax and Formatting
For syntax and formatting, follow the Ruby Style Guide. Ruby’s expressive syntax can make your code cleaner—use constructs like `unless`, `||=`, and `&.` when appropriate. When it comes to strings, prefer single quotes unless you need interpolation.

### Error Handling and Validation
Error handling is crucial. Use exceptions for exceptional cases, not as a control flow mechanism. Make sure you implement proper error logging and offer user-friendly messages. In your models, utilize ActiveModel validations, and handle errors gracefully in your controllers. Display appropriate flash messages to keep users informed.

### UI and Styling
For the user interface, Hotwire (Turbo and Stimulus) can help create dynamic interactions similar to single-page applications. Make your designs responsive with Tailwind CSS. Also, Rails view helpers and partials can help you maintain clean, DRY views.

### Performance Optimization
Performance is key, so effectively use database indexing. Consider caching strategies, such as fragment caching and Russian Doll caching, to improve speed. Eager loading can help you avoid N+1 queries, and optimizing your database queries with includes, joins, or select will keep everything running smoothly.

### Key Conventions
Stick to RESTful routing conventions for a more intuitive structure. Use concerns to share behavior across models or controllers. For any complex business logic, consider implementing service objects. Background jobs, like those with Sidekiq, can handle time-consuming tasks without slowing down your application.

### Testing
Testing is vital, so write comprehensive tests using RSpec or Minitest. Follow TDD or BDD practices to help guide your development. Using factories, such as FactoryBot, can simplify generating test data.

### Security
Lastly, security matters. Implement proper authentication and authorization with tools like Devise and Pundit. Use strong parameters in your controllers to protect your data. Always stay vigilant against common web vulnerabilities, including XSS, CSRF, and SQL injection.

For more details, check out the official Ruby on Rails guides. They provide solid guidance on best practices for routing, controllers, models, views, and other components. Happy coding!