---
title: "Next.js React Redux TypeScript Best Practices"
description: "This guide presents best practices, conventions, and standards for development using modern web technologies such as ReactJS, NextJS, Redux, and TypeScript."
category: "rules"
tags: ["Next.js", "React", "Redux", "TypeScript", "Best Practices"]
tech_stack: ["shadcn", "radix", "tailwind", "nuqs"]
---

You’re well-versed in TypeScript, React, Next.js, Redux, and modern UI frameworks like Shadcn UI and Tailwind CSS. Let’s break down your development philosophy and best practices for a smoother coding experience.

### Development Philosophy
First off, focus on writing clean, maintainable, and scalable code. Stick to **SOLID** principles to improve your software design. Embrace **functional** and **declarative** programming styles over **imperative** ones. Always prioritize **type safety** and **static analysis**. Lastly, adopt **component-driven development** to enhance modularity.

### Code Implementation Guidelines
#### Planning Phase
Before diving into coding, kick things off with a detailed planning phase. Draft comprehensive **pseudocode** to guide your implementation. Make sure to document your component architecture and data flow clearly. Don’t forget to anticipate edge cases and possible errors during this stage.

### Code Style
When it comes to code style, use **tabs** for indentation. Stick with **single quotes** for strings unless you need to escape something. You can skip semicolons unless they clarify your code. Keep your code clean by removing unused variables and inserting a space after keywords and before function declaration parentheses. Use **strict equality** (`===`) for comparisons. Space out your infix operators and add space after commas for better readability. Keep `else` statements on the same line as their closing curly braces, and always use curly braces for multi-line `if` statements. Be consistent with error parameters in callbacks, limit line length to **80 characters**, and use trailing commas in multiline objects and arrays for clearer diffs.

### Naming Conventions
#### General Rules
Let’s discuss naming conventions. Use **PascalCase** for:
- Components
- Type definitions
- Interfaces

Use **kebab-case** for:
- Directory names (e.g., `components/auth-wizard`)
- File names (e.g., `user-profile.tsx`)

For:
- Variables
- Functions
- Methods
- Hooks
- Properties
- Props

Use **camelCase**. And for:
- Environment variables
- Constants
- Global configurations

Use **UPPERCASE**.

#### Specific Naming Patterns
When naming, prefix event handlers with `handle`, such as `handleClick` and `handleSubmit`. Start boolean variables with verbs like `isLoading`, `hasError`, or `canSubmit`. For custom hooks, use the prefix `use`, like `useAuth` or `useForm`. Avoid abbreviations except for common terms like `err` (error), `req` (request), `res` (response), `props` (properties), and `ref` (reference).

### React Best Practices
#### Component Architecture
In React, opt for functional components with TypeScript interfaces. Define your components using the `function` keyword and extract reusable logic into custom hooks. Proper component composition is key, and don’t hesitate to use `React.memo()` to improve performance. Remember to clean up in your `useEffect` hooks.

#### React Performance Optimization
For performance, use `useCallback` to memoize your callback functions and `useMemo` for expensive computations. Avoid inline function definitions in JSX to prevent unnecessary re-renders. Code splitting using dynamic imports is a smart choice, and always ensure that you use proper key props in lists—avoid using the index as a key.

### Next.js Best Practices
#### Core Concepts
In Next.js, utilize the **App Router** for routing. Manage metadata effectively and implement appropriate caching strategies. Use error boundaries to handle errors gracefully.

#### Components and Features
Leverage Next.js built-in components like:
- **Image** for optimized images
- **Link** for client-side navigation
- **Script** for external scripts
- **Head** for managing metadata

Implement loading states properly and choose the right data fetching methods.

#### Server Components
Default to using **Server Components**. Use URL query parameters for data fetching and managing server state. Only use the `'use client'` directive when necessary, such as for event listeners, browser APIs, state management, or client-only libraries.

### TypeScript Implementation
Enable strict mode for better type checking. Clearly define interfaces for your component props, state, and Redux state structure. Use type guards to safely handle potential undefined or null values. Apply generics where flexibility is needed, and take advantage of TypeScript utility types (Partial, Pick, Omit) for cleaner, reusable code. Prefer interfaces over types for object structures, especially when extending, and use mapped types to create variations of existing types dynamically.

### UI and Styling
#### Component Libraries
Use **Shadcn UI** for consistent and accessible component design. Integrate **Radix UI** primitives for customizable, accessible UI elements. Apply composition patterns to create modular and reusable components.

#### Styling Guidelines
For styling, adopt **Tailwind CSS** for utility-first, maintainable design. Always think mobile-first and responsive to ensure flexibility across devices. Implement dark mode using CSS variables or Tailwind’s built-in features. Ensure your color contrast ratios meet accessibility standards, and maintain consistent spacing values for visual harmony. Define CSS variables for theme colors and spacing to support easy theming and maintenance.

### State Management
#### Local State
Manage local state with `useState`, and turn to `useReducer` for complex state handling. Use `useContext` for shared state across components and ensure proper state initialization.

#### Global State
For global state, use **Redux Toolkit**. Utilize `createSlice` to define state, reducers, and actions together. Avoid `createReducer` and `createAction` unless absolutely necessary. Normalize your state structure to keep it flat and use selectors for state access. Also, avoid large, all-encompassing slices; separate concerns by feature.

### Error Handling and Validation
#### Form Validation
For form validation, use **Zod** for schema validation. Provide clear error messages to give users feedback, and leverage appropriate form libraries, like **React Hook Form**.

#### Error Boundaries
Implement error boundaries to catch and handle errors gracefully in React component trees. Log caught errors to an external service, like **Sentry**, to help with tracking and debugging. Make sure to design user-friendly fallback UIs to keep users informed when errors happen, ensuring a smooth experience.