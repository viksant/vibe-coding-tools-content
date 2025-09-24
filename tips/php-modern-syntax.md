---
title: "Request PHP Modern Syntax with Type Declarations"
description: "Get modern PHP code with type hints and object-oriented patterns"
category: "tips-tricks"
tags: ["php", "type-declarations", "modern-php", "oop", "psr"]
tech_stack: ["php"]
---

To keep your PHP code up to date and easy to maintain, always ask for code that uses PHP 8 or higher. This includes features like type declarations and object-oriented patterns. These elements not only make your code clearer but also help prevent runtime errors.

1. **Specify PHP Version**: When you request code, be clear that you need PHP 8 or newer.
   - For example, you might say: `Please provide PHP 8 code with type declarations.`

2. **Request Type Declarations**: Make sure to ask for specific type hints for function parameters and return types.
   - You can say: `Include type hints for all parameters and return types.`

3. **Incorporate Nullable and Union Types**: Mention that nullable types and union types should be used where appropriate.
   - A good request might be: `Use nullable types for optional parameters and union types for multiple accepted types.`

4. **Follow PSR Standards**: Ask that the code adheres to PHP Standards Recommendations (PSR) for style and structure.
   - You could request: `Ensure the code follows PSR-12 for formatting and PSR-4 for autoloading.`

5. **Ask for Object-Oriented Patterns**: Encourage the use of modern object-oriented programming practices, such as interfaces and traits.
   - An example request is: `Utilize interfaces and traits to promote code reusability.`

By following these steps, you’ll receive PHP code that is clean, easy to read, and in line with modern standards.

### Why It Works
Using the latest PHP features makes your code easier to read, maintain, and improve performance. This is especially useful when working in teams or on larger projects where consistent coding practices matter.

### Quick Examples
- **Before**: 
  ```php
  function calculate($num) {
      return $num * 2;
  }
  ```
- **After**: 
  ```php
  function calculate(int $num): int {
      return $num * 2;
  }
  ```

- **Before**: 
  ```php
  function getUser($id) {
      // logic
  }
  ```
- **After**: 
  ```php
  function getUser(?int $id): User {
      // logic
  }
  ```

### Common Mistakes
- **Not specifying PHP version**: Always mention the required PHP version to avoid outdated code. 
  - Fix: Include `Please provide PHP 8 code` in your request.
  
- **Ignoring type hints**: Not asking for type declarations can lead to confusion in your code.
  - Fix: Explicitly request `Include type hints for all parameters and return types.`
  
- **Neglecting PSR standards**: Not following PSR can create a messy code style.
  - Fix: Request `Ensure the code follows PSR-12 for formatting.`
  
- **Overlooking OOP practices**: Avoid using procedural code when object-oriented programming would work better.
  - Fix: Ask for `Utilize interfaces and traits for better structure.`