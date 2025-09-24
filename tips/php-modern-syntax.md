---
title: "Request PHP Modern Syntax with Type Declarations"
description: "Get modern PHP code with type hints and object-oriented patterns"
category: "tips-tricks"
tags: ["php", "type-declarations", "modern-php", "oop", "psr"]
tech_stack: ["php"]
---

To ensure your PHP code is modern and maintainable, always request code that utilizes PHP 8+ features, including type declarations and object-oriented patterns. This approach enhances code clarity and reduces runtime errors.

1. **Specify PHP Version**: When asking for code, clearly state you need PHP 8 or higher.
   - Example request: `Please provide PHP 8 code with type declarations.`
   
2. **Request Type Declarations**: Ask for specific type hints for function parameters and return types.
   - Example request: `Include type hints for all parameters and return types.`

3. **Incorporate Nullable and Union Types**: Specify the need for nullable types and union types where applicable.
   - Example request: `Use nullable types for optional parameters and union types for multiple accepted types.`

4. **Follow PSR Standards**: Request adherence to PHP Standards Recommendations (PSR) for coding style and structure.
   - Example request: `Ensure the code follows PSR-12 for formatting and PSR-4 for autoloading.`

5. **Ask for Object-Oriented Patterns**: Encourage the use of modern OOP practices, such as interfaces and traits.
   - Example request: `Utilize interfaces and traits to promote code reusability.`

Expected result: You will receive PHP code that is clean, efficient, and adheres to modern standards.

### Why It Works
Using modern PHP features improves code readability, maintainability, and performance. This is especially beneficial in collaborative environments or large projects where consistent coding standards are crucial.

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
  
- **Ignoring type hints**: Failing to ask for type declarations can lead to ambiguous code.
  - Fix: Explicitly request `Include type hints for all parameters and return types.`
  
- **Neglecting PSR standards**: Not adhering to PSR can result in inconsistent code style.
  - Fix: Request `Ensure the code follows PSR-12 for formatting.`
  
- **Overlooking OOP practices**: Avoid procedural code when OOP is more suitable.
  - Fix: Ask for `Utilize interfaces and traits for better structure.`