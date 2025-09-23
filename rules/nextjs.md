---
title: "Next.js React Redux TypeScript Best Practices"
description: "This guide presents best practices, conventions, and standards for development using modern web technologies such as ReactJS, NextJS, Redux, and TypeScript."
category: "rules"
tags: ["Next.js", "React", "Redux", "TypeScript", "Best Practices"]
tech_stack: ["shadcn", "radix", "tailwind", "nuqs"]
---

You are an expert in TypeScript, React, Next.js, Redux, and modern UI frameworks like Shadcn UI and Tailwind CSS.

### Development Philosophy
- Write clean, maintainable, and scalable code.
- Adhere to **SOLID** principles for better software design.
- Favor **functional** and **declarative** programming patterns over **imperative** styles.
- Prioritize **type safety** and **static analysis**.
- Embrace **component-driven development** for modularity.

### Code Implementation Guidelines
#### Planning Phase
- Initiate projects with a detailed step-by-step planning process.
- Draft comprehensive **pseudocode** prior to implementation.
- Document component architecture and data flow clearly.
- Anticipate edge cases and error scenarios during planning.

### Code Style
- Use **tabs** for indentation.
- Prefer **single quotes** for strings, except when escaping is necessary.
- Omit semicolons unless they are required for disambiguation.
- Remove unused variables to maintain code cleanliness.
- Insert a space after keywords and before function declaration parentheses.
- Always use **strict equality** (`===`) instead of loose equality (`==`).
- Space infix operators and add space after commas for readability.
- Keep `else` statements on the same line as their closing curly braces.
- Utilize curly braces for multi-line `if` statements.
- Handle error parameters in callbacks consistently.
- Limit line length to **80 characters** for better readability.
- Use trailing commas in multiline object and array literals for cleaner diffs.

### Naming Conventions
#### General Rules
- Use **PascalCase** for:
  - Components
  - Type definitions
  - Interfaces
- Use **kebab-case** for:
  - Directory names (e.g., `components/auth-wizard`)
  - File names (e.g., `user-profile.tsx`)
- Use **camelCase** for:
  - Variables
  - Functions
  - Methods
  - Hooks
  - Properties
  - Props
- Use **UPPERCASE** for:
  - Environment variables
  - Constants
  - Global configurations

#### Specific Naming Patterns
- Prefix event handlers with `handle`: `handleClick`, `handleSubmit`.
- Prefix boolean variables with verbs: `isLoading`, `hasError`, `canSubmit`.
- Prefix custom hooks with `use`: `useAuth`, `useForm`.
- Use full words instead of abbreviations, except for common terms like:
  - `err` (error)
  - `req` (request)
  - `res` (response)
  - `props` (properties)
  - `ref` (reference)

### React Best Practices
#### Component Architecture
- Utilize functional components with TypeScript interfaces.
- Define components using the `function` keyword.
- Extract reusable logic into custom hooks.
- Implement proper component composition.
- Use `React.memo()` strategically for performance optimization.
- Ensure proper cleanup in `useEffect` hooks.

#### React Performance Optimization
- Use `useCallback` for memoizing callback functions.
- Implement `useMemo` for expensive computations.
- Avoid inline function definitions in JSX to prevent unnecessary re-renders.
- Employ code splitting using dynamic imports.
- Ensure proper key props in lists (avoid using index as key).

### Next.js Best Practices
#### Core Concepts
- Utilize the **App Router** for routing.
- Manage metadata effectively.
- Implement appropriate caching strategies.
- Use error boundaries to handle errors gracefully.

#### Components and Features
- Leverage Next.js built-in components:
  - **Image** component for optimized images.
  - **Link** component for client-side navigation.
  - **Script** component for external scripts.
  - **Head** component for managing metadata.
- Implement loading states properly.
- Use appropriate data fetching methods.

#### Server Components
- Default to using **Server Components**.
- Utilize URL query parameters for data fetching and server state management.
- Use the `'use client'` directive only when absolutely necessary, such as for:
  - Event listeners
  - Browser APIs
  - State management
  - Client-side-only libraries

### TypeScript Implementation
- Enable strict mode for better type checking.
- Define clear interfaces for component props, state, and Redux state structure.
- Use type guards to safely handle potential undefined or null values.
- Apply generics to functions, actions, and slices where type flexibility is needed.
- Utilize TypeScript utility types (Partial, Pick, Omit) for cleaner, reusable code.
- Prefer interfaces over types for defining object structures, especially when extending.
- Use mapped types for creating variations of existing types dynamically.

### UI and Styling
#### Component Libraries
- Use **Shadcn UI** for consistent, accessible component design.
- Integrate **Radix UI** primitives for customizable, accessible UI elements.
- Apply composition patterns to create modular, reusable components.

#### Styling Guidelines
- Use **Tailwind CSS** for utility-first, maintainable styling.
- Design with a mobile-first, responsive approach for flexibility across devices.
- Implement dark mode using CSS variables or Tailwind’s dark mode features.
- Ensure color contrast ratios meet accessibility standards for readability.
- Maintain consistent spacing values to establish visual harmony.
- Define CSS variables for theme colors and spacing to support easy theming and maintainability.

### State Management
#### Local State
- Use `useState` for component-level state management.
- Implement `useReducer` for handling complex state.
- Use `useContext` for shared state across components.
- Ensure proper state initialization.

#### Global State
- Utilize **Redux Toolkit** for global state management.
- Use `createSlice` to define state, reducers, and actions together.
- Avoid using `createReducer` and `createAction` unless necessary.
- Normalize state structure to prevent deeply nested data.
- Use selectors to encapsulate state access.
- Avoid large, all-encompassing slices; separate concerns by feature.

### Error Handling and Validation
#### Form Validation
- Use **Zod** for schema validation.
- Implement clear error messages for user feedback.
- Utilize appropriate form libraries (e.g., **React Hook Form**).

#### Error Boundaries
- Implement error boundaries to catch and handle errors in React component trees gracefully.
- Log caught errors to an external service (e.g., **Sentry**) for tracking and debugging.
- Design user-friendly fallback UIs to inform users when errors occur, ensuring a smooth user experience.