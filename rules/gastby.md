---
title: "Gatsby Cursor Guidelines"
description: "You are an expert in TypeScript, Gatsby, React, and Tailwind. This document outlines best practices for code style, naming conventions, and TypeScript usage."
category: "rules"
tags: ["Gatsby", "React", "GraphQL", "Tailwind", "TypeScript"]
tech_stack: ["gatsby", "react", "graphql", "tailwind", "typescript"]
---

You have a solid foundation in TypeScript, Gatsby, React, and Tailwind. Let’s explore how to write clean and effective code.

### Code Style and Structure

Keep your TypeScript code concise and clear. Lean towards functional and declarative programming styles instead of using classes. Focus on iterating and modularizing your code to cut down on duplication. Choose descriptive variable names that include auxiliary verbs, like `isLoaded` or `hasError`. Organize your files in this order: start with exported pages or components, then GraphQL queries, followed by helper functions, static content, and type definitions.

### Naming Conventions

When it comes to naming, prefer using named exports for your components and utility functions. For GraphQL query files, add a `use` prefix, such as `useSiteMetadata.ts`, to make it clear that these are hooks.

### TypeScript Usage

Always use TypeScript for your code, and when defining shapes, favor interfaces over types. Skip using enums; instead, stick with objects or maps. It's a good idea to avoid the `any` type to keep your code type-safe.

#### Example of Descriptive Variable Naming

Here’s a quick example of how to name your variables:

```typescript
const isDataFetched = true;
const hasErrorOccurred = false;
```

#### Example of File Structure

Here’s a suggested structure for your files:

```
src/
  components/
    MyComponent.tsx
  queries/
    useSiteMetadata.ts
  helpers/
    formatDate.ts
  types/
    userTypes.ts
```

With these guidelines, you’ll create a codebase that is not only easy to read but also easy to maintain. Happy coding!