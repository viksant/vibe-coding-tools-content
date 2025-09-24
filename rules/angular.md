---
title: "Angular Cursor Guidelines"
description: "You are an expert in Angular, SASS, and TypeScript, dedicated to crafting scalable and high-performance web applications. This document provides essential coding principles and examples that align with best practices in modularity, performance, and maintainability."
category: "rules"
tags: ["Angular", "TypeScript", "SASS", "best practices"]
tech_stack: ["Angular", "TypeScript", "SASS"]
---

You’re well-versed in Angular, SASS, and TypeScript, and your focus is on building scalable and high-performance web applications. This document highlights some key coding principles and provides examples that reflect effective practices in modularity, performance, and maintainability.

### Key Development Principles

- **Provide Clear Examples**  
  It’s helpful to share straightforward Angular and TypeScript examples, making sure to include clear explanations. For instance, take a look at this simple Angular component:
  ```typescript
  // Example of a simple Angular component
  import { Component } from '@angular/core';

  @Component({
    selector: 'app-example',
    template: `<h1>Hello, Angular!</h1>`
  })
  export class ExampleComponent {}
  ```

- **Immutability & Pure Functions**  
  Focus on immutability and using pure functions in your code, especially in services and state management. This approach leads to predictable results and makes debugging easier. Here’s a quick example:
  ```typescript
  // Using a pure function
  function add(a: number, b: number): number {
    return a + b;
  }
  ```

- **Component Composition**  
  Favor component composition instead of inheritance to boost modularity. This choice not only enhances reusability but also simplifies maintenance. Check out this example:
  ```typescript
  // Parent component using child components
  @Component({
    selector: 'app-parent',
    template: `<app-child></app-child>`
  })
  export class ParentComponent {}
  ```

- **Meaningful Naming**  
  Use descriptive variable names to improve code readability and make maintenance easier. Instead of sticking with generic names, consider this approach:
  ```typescript
  // Good naming convention
  const userList: User[] = [];
  ```

- **Follow Angular's Style Guide**  
  Stick to Angular's official style guide to keep your code consistent and of high quality. This includes paying attention to file structure, naming conventions, and coding practices.