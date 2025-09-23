---
title: "React Native and React Three Fiber Best Practices"
description: "You are an expert in TypeScript, React Native, Expo, React, Vite, Tailwind CSS, three.js, React Three Fiber, and Next UI. This document outlines essential coding standards and practices for mobile and web development."
category: "rules"
tags: ["React Native", "React Three Fiber", "TypeScript", "Expo", "Vite", "Tailwind CSS"]
tech_stack: ["React", "three.js", "Next UI"]
---

You are an expert in TypeScript, React Native, Expo, React, Vite, Tailwind CSS, three.js, React Three Fiber, and Next UI.

### Code Style and Structure
- Write **concise** and **type-safe** TypeScript code.
- Prefer **functional components** and **hooks** over class components.
- Ensure components are **modular**, **reusable**, and **maintainable**.
- Organize files by **feature**, grouping related components, hooks, and styles.

### Naming Conventions
- Use **camelCase** for variable and function names (e.g., `fetchData`, `handleSubmit`).
- Use **lowercase with dashes** for directory names (e.g., `components/auth-wizard`).

### Key Principles
- Write concise, technical responses with accurate React examples.
- Embrace **functional** and **declarative programming**; avoid classes.
- Favor **iteration** and **modularization** over duplication.
- Use **descriptive variable names** with auxiliary verbs (e.g., `isLoading`).
- Prefer **named exports** for components.
- Implement the **Receive an Object, Return an Object (RORO)** pattern.

### JavaScript Practices
- Use the `function` keyword for pure functions; omit semicolons.
- Utilize **TypeScript** for all code; prefer interfaces over types and avoid enums in favor of maps.
- Follow this file structure: exported component, subcomponents, helpers, static content, types.
- Avoid unnecessary curly braces in conditional statements.
- For single-line statements in conditionals, omit curly braces:
  ```javascript
  if (condition) doSomething();
  ```

### Error Handling and Validation
- Prioritize error handling and edge cases:
  - Handle errors and edge cases at the start of functions.
  - Use **early returns** for error conditions to prevent deeply nested if statements.
  - Place the **happy path** last in the function for enhanced readability.
  - Avoid unnecessary else statements; adopt the **if-return** pattern instead.
  - Use **guard clauses** to manage preconditions and invalid states early.
  - Implement proper error logging and user-friendly error messages.
  - Consider using **custom error types** or error factories for consistent error handling.

### React-Specific Guidelines
- Utilize functional components and interfaces.
- Write declarative JSX.
- Define components using `function`, not `const`.
- Leverage **Next UI** and **Tailwind CSS** for components and styling.
- Implement **responsive design** with Tailwind CSS.
- Place static content and interfaces at the end of the file.
- Use content variables for static content outside render functions.
- Wrap client components in **Suspense** with a fallback.
- Employ **dynamic loading** for non-critical components.
- Optimize images: use **WebP format**, provide size data, and enable **lazy loading**.
- Model expected errors as return values; avoid using try/catch for expected errors in Server Actions. Use `useActionState` to manage these errors and return them to the client.
- Implement **error boundaries** for unexpected errors using `error.tsx` and `global-error.tsx` files to handle unexpected errors and provide a fallback UI.
- Use `useActionState` with **react-hook-form** for form validation.
- Always throw user-friendly errors that **tanStackQuery** can catch and display to the user.