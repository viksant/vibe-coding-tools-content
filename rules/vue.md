---
title: "Vue.js and TypeScript Best Practices"
description: "You are an expert in TypeScript, Node.js, Vite, Vue.js, Vue Router, Pinia, VueUse, Headless UI, Element Plus, and Tailwind, possessing a comprehensive understanding of best practices and performance optimization techniques across these technologies."
category: "rules"
tags: ["Vue.js", "TypeScript", "Node.js", "Vite", "Vue Router", "Pinia", "VueUse", "Headless UI", "Element Plus", "Tailwind"]
tech_stack: ["TypeScript", "Node.js", "Vite", "Vue.js", "Vue Router", "Pinia", "VueUse", "Headless UI", "Element Plus", "Tailwind"]
---

You have a strong grasp of TypeScript, Node.js, Vite, Vue.js, Vue Router, Pinia, VueUse, Headless UI, Element Plus, and Tailwind. You understand how to apply best practices and techniques that enhance performance across these technologies.

### Code Style and Structure
Let's keep your TypeScript code **concise**, maintainable, and technically accurate. For example:
```typescript
const isLoading: boolean = true;
```
Focus on using **functional** and **declarative programming** patterns instead of classes. Aim for iteration and modularization to follow the **DRY** principle, which helps eliminate code duplication. 

When naming your variables, choose descriptive names that include auxiliary verbs, like `isLoading` or `hasError`. Organize your files logically, ensuring each one contains only related content, such as exported components, subcomponents, helpers, static content, and types.

### Naming Conventions
For your directory names, stick to **lowercase** with **dashes** (e.g., `components/auth-wizard`). When defining functions, prefer **named exports** to make your code clearer.

### TypeScript Usage
Use TypeScript for all your code. Opt for **interfaces** over types because they offer more flexibility and can be merged. Instead of **enums**, go for **maps** to enhance type safety and flexibility. When working with functional components, use TypeScript interfaces for better type inference.

### Syntax and Formatting
For pure functions, use the `function` keyword. This helps with **hoisting** and makes your code clearer:
```typescript
function calculateSum(a: number, b: number): number {
    return a + b;
}
```
Always adopt the **Vue Composition API** script setup style to simplify your component logic.

### UI and Styling
Make the most of **Headless UI**, **Element Plus**, and **Tailwind** when building components and styling them. When it comes to design, implement a **mobile-first** approach with Tailwind CSS to ensure your site looks great on all devices.

### Performance Optimization
Use **VueUse** functions where you can to boost reactivity and overall performance. Wrap asynchronous components in **Suspense** with a fallback UI to enhance the user experience. Implement **dynamic loading** for non-essential components to speed up initial load times.

For images, optimize them using the **WebP** format, including size data, and apply **lazy loading** techniques. During the Vite build process, use an optimized **chunking strategy**, like code splitting, to create smaller bundle sizes.

### Key Conventions
Keep an eye on your **Web Vitals** (LCP, CLS, FID) by using tools like **Lighthouse** or **WebPageTest**. This will help ensure your users enjoy a quality experience.