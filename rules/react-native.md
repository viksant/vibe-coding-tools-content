---
title: "React Native and React Three Fiber Best Practices"
description: "You are an expert in TypeScript, React Native, Expo, React, Vite, Tailwind CSS, three.js, React Three Fiber, and Next UI. This document outlines essential coding standards and practices for mobile and web development."
category: "rules"
tags: ["React Native", "React Three Fiber", "TypeScript", "Expo", "Vite", "Tailwind CSS"]
tech_stack: ["React", "three.js", "Next UI"]
---

You have a solid foundation in TypeScript, React Native, Expo, React, Vite, Tailwind CSS, three.js, React Three Fiber, and Next UI. Let’s dive into some best practices to keep your code clean and effective.

### Code Style and Structure
Start by writing TypeScript code that is both clear and type-safe. Functional components and hooks should be your go-to choices instead of class components. Keep your components modular, reusable, and maintainable. Organize your files by feature, grouping related components, hooks, and styles together for better clarity.

### Naming Conventions
When it comes to naming, use camelCase for your variable and function names. For example, you might have names like `fetchData` or `handleSubmit`. For directory names, stick to lowercase with dashes, such as `components/auth-wizard`.

### Key Principles
Aim to write concise and technical responses with precise React examples. Embrace functional and declarative programming, steering clear of classes. Focus on iteration and modularization rather than duplicating code. Use descriptive variable names that include auxiliary verbs, like `isLoading`. It’s also a good idea to prefer named exports for your components. Don’t forget to implement the Receive an Object, Return an Object (RORO) pattern for clarity.

### JavaScript Practices
For pure functions, use the `function` keyword and leave out semicolons where possible. Always use TypeScript for your code; prefer interfaces over types and choose maps instead of enums. Follow this structure: start with the exported component, then subcomponents, helpers, static content, and finally, types. Keep your conditional statements clean by avoiding unnecessary curly braces. For single-line statements, you can skip the curly braces entirely:
```javascript
if (condition) doSomething();
```

### Error Handling and Validation
Make error handling and edge cases a priority. Handle these situations right at the start of your functions. Using early returns for error conditions helps you avoid deeply nested if statements. Place the happy path at the end of the function to improve readability. Instead of using unnecessary else statements, consider the if-return pattern. Use guard clauses to manage preconditions and invalid states early on. Implement proper error logging and ensure your error messages are user-friendly. It might also be helpful to consider using custom error types or error factories for consistent handling.

### React-Specific Guidelines
Stick with functional components and interfaces. Write declarative JSX and define your components using the `function` keyword instead of `const`. Use Next UI and Tailwind CSS for your components and styling. Make sure your designs are responsive with Tailwind CSS. Keep static content and interfaces towards the end of your file, and use content variables for static content outside of render functions. Wrap client components in Suspense with a fallback to manage loading states. For non-critical components, employ dynamic loading. Optimize your images by using the WebP format, providing size data, and enabling lazy loading.

When dealing with expected errors, model them as return values. Avoid using try/catch blocks for these errors in Server Actions. Instead, leverage `useActionState` to manage these errors and pass them back to the client. Implement error boundaries for unexpected errors by using `error.tsx` and `global-error.tsx` files. This will help you handle unforeseen issues and provide a fallback UI. For form validation, use `useActionState` together with react-hook-form. Always throw user-friendly errors that tanStackQuery can catch and display to users effectively.