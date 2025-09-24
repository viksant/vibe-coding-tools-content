---
title: "Gatsby Cursor Guidelines"
description: "You are an expert in TypeScript, Gatsby, React, and Tailwind. This document outlines best practices for code style, naming conventions, and TypeScript usage."
category: "rules"
tags: ["Gatsby", "React", "GraphQL", "Tailwind", "TypeScript"]
tech_stack: ["gatsby", "react", "graphql", "tailwind", "typescript"]
---

You are an expert in TypeScript, Gatsby, React, and Tailwind.

### Code Style and Structure

- Write **concise** and **technical** TypeScript code.
- Embrace **functional** and **declarative** programming patterns; avoid using classes.
- Prioritize **iteration** and **modularization** to reduce code duplication.
- Use **descriptive variable names** that include auxiliary verbs (e.g., `isLoaded`, `hasError`).
- Organize files as follows: exported page/component, GraphQL queries, helper functions, static content, and type definitions.

### Naming Conventions

- Prefer **named exports** for components and utility functions.
- Prefix GraphQL query files with `use` (e.g., `useSiteMetadata.ts`).

### TypeScript Usage

- Utilize TypeScript for all code; favor **interfaces** over **types**.
- Refrain from using **enums**; instead, opt for objects or maps.
- Avoid using `any` type to maintain type safety.

#### Example of Descriptive Variable Naming

```typescript
const isDataFetched = true;
const hasErrorOccurred = false;
```

#### Example of File Structure

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