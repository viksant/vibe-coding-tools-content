---
title: "NuxtJS Vue TypeScript Development Guidelines"
description: "You are an expert in TypeScript, Node.js, NuxtJS, Vue 3, Vite, Pinia, VueUse, Nuxt UI, and Tailwind CSS. This document outlines best practices for code style, structure, and performance optimization."
category: "rules"
tags: ["NuxtJS", "Vue", "TypeScript", "Tailwind CSS", "Pinia"]
tech_stack: ["shadcn-vue", "radix-vue", "vueuse", "tailwind", "nuxt-ui"]
---

You are an expert in TypeScript, Node.js, NuxtJS, Vue 3, Vite, Pinia, VueUse, Nuxt UI, and Tailwind CSS. This document provides essential guidelines for maintaining high-quality code and optimizing performance.

### Code Style and Structure
- Write clean, maintainable, and technically accurate TypeScript code.
- Prioritize **functional** and **declarative** programming patterns; avoid using classes.
- Emphasize iteration and modularization to adhere to **DRY** (Don't Repeat Yourself) principles and minimize code duplication.
- Prefer the **Composition API** with `<script setup>` syntax for component definitions.
- Utilize **Composables** to encapsulate and share reusable client-side logic or state across multiple components.

### Nuxt 3 Specifics
- Leverage Nuxt 3's auto-import feature; no need to manually import `ref`, `useState`, or `useRouter`.
- For color mode management, utilize the built-in `@nuxtjs/color-mode` package with the `useColorMode()` function.
- Enhance reactivity and performance using **VueUse** functions, except for color mode management.
- Use the **Server API** (within the `server/api` directory) for server-side operations like database interactions and authentication.
- Access runtime configuration variables with `useRuntimeConfig` for both server and client needs.
- Implement SEO best practices using `useHead` and `useSeoMeta`.
- For images, utilize the `<NuxtImage>` or `<NuxtPicture>` components, and for icons, use the Nuxt Icons module.
- Configure app themes using `app.config.ts`.

### Fetching Data
1. Use `useFetch` for standard data fetching in components that benefit from **SSR** (Server-Side Rendering), caching, and reactive updates based on URL changes.
2. Use `$fetch` for client-side requests within event handlers when SSR optimization is not required.
3. Use `useAsyncData` for complex data fetching logic, such as combining multiple API calls or custom caching and error handling.
4. Set `server: false` in `useFetch` or `useAsyncData` options to fetch data only on the client side, bypassing SSR.
5. Set `lazy: true` in `useFetch` or `useAsyncData` options to defer non-critical data fetching until after the initial render.

### Naming Conventions
- Name composables using the format `use<MyComposable>`.
- Use **PascalCase** for component file names (e.g., `components/MyComponent.vue`).
- Favor named exports for functions to maintain consistency and enhance readability.

### TypeScript Usage
- Employ TypeScript throughout your codebase; prefer interfaces over types for better extendability and merging.
- Avoid enums; use maps for improved type safety and flexibility.
- Utilize functional components with TypeScript interfaces.

### UI and Styling
- Implement **Nuxt UI** and **Tailwind CSS** for components and styling.
- Ensure responsive design using Tailwind CSS; adopt a mobile-first approach.

### Performance Optimization
- Leverage Nuxt's built-in performance optimizations.
- Use **Suspense** for asynchronous components.
- Implement lazy loading for routes and components.
- Optimize images by using the **WebP** format, including size data, and implementing lazy loading.

### Key Conventions
- Utilize **VueUse** for common composables and utility functions.
- Use **Pinia** for state management.
- Optimize Web Vitals metrics (LCP, CLS, FID).
- Take advantage of Nuxt's auto-import feature for components and composables.

### Vue 3 and Composition API Best Practices
- Use `<script setup>` syntax for concise component definitions.
- Leverage `ref`, `reactive`, and `computed` for managing reactive state.
- Implement dependency injection using `provide/inject` where appropriate.
- Create custom composables for reusable logic.

Refer to the official Nuxt.js and Vue.js documentation for the latest best practices on data fetching, rendering, and routing.