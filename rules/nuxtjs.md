---
title: "NuxtJS Vue TypeScript Development Guidelines"
description: "You are an expert in TypeScript, Node.js, NuxtJS, Vue 3, Vite, Pinia, VueUse, Nuxt UI, and Tailwind CSS. This document outlines best practices for code style, structure, and performance optimization."
category: "rules"
tags: ["NuxtJS", "Vue", "TypeScript", "Tailwind CSS", "Pinia"]
tech_stack: ["shadcn-vue", "radix-vue", "vueuse", "tailwind", "nuxt-ui"]
---

You have a solid grasp of TypeScript, Node.js, NuxtJS, Vue 3, Vite, Pinia, VueUse, Nuxt UI, and Tailwind CSS. This guide will help you maintain high-quality code and boost performance.

### Code Style and Structure
Start by writing clean and maintainable TypeScript code. Focus on functional and declarative programming patterns instead of classes. Keep your code modular and avoid repetition by following the DRY principle. The Composition API with `<script setup>` syntax is your friend for defining components. Use Composables to wrap reusable client-side logic or state that multiple components can share.

### Nuxt 3 Specifics
Take advantage of Nuxt 3’s auto-import feature. You'll find no need to manually import `ref`, `useState`, or `useRouter`. For managing color modes, use the built-in `@nuxtjs/color-mode` package along with the `useColorMode()` function. Boost your app's reactivity and performance with VueUse functions, except when handling color modes. 

For server-side tasks like database interactions and authentication, use the Server API located in the `server/api` directory. Access runtime configuration variables using `useRuntimeConfig`, which works for both server and client needs. Implement SEO best practices with `useHead` and `useSeoMeta`. When it comes to images, make use of `<NuxtImage>` or `<NuxtPicture>`, and for icons, rely on the Nuxt Icons module. Don’t forget to set app themes in `app.config.ts`.

### Fetching Data
When it comes to data fetching, here’s a simple breakdown:
1. Use `useFetch` for standard data fetching in components that benefit from SSR, caching, and responsive updates based on URL changes.
2. Use `$fetch` for client-side requests inside event handlers when you don’t need SSR.
3. Use `useAsyncData` for more complex data fetching, like combining multiple API calls or handling custom caching and errors.
4. If you want to fetch data only on the client-side, set `server: false` in `useFetch` or `useAsyncData` options.
5. If you want to delay non-critical data fetching until after the initial render, set `lazy: true` in those options.

### Naming Conventions
When naming your composables, use the format `use<MyComposable>`. Stick to PascalCase for your component file names, like `components/MyComponent.vue`. Also, prefer named exports for functions to keep things consistent and readable.

### TypeScript Usage
Incorporate TypeScript across your codebase. Favor interfaces over types for better extendability and merging. Avoid enums; instead, use maps to improve type safety and flexibility. Functional components with TypeScript interfaces work well together.

### UI and Styling
Use Nuxt UI and Tailwind CSS for your components and styling. Make sure your designs are responsive, following a mobile-first approach with Tailwind CSS.

### Performance Optimization
Take advantage of Nuxt's built-in performance features. Use Suspense for asynchronous components and implement lazy loading for routes and components. Optimize your images by using the WebP format, including size data, and ensure lazy loading is in place.

### Key Conventions
Use VueUse for common composables and utility functions, and rely on Pinia for state management. Keep an eye on Web Vitals metrics like LCP, CLS, and FID. Don't forget to utilize Nuxt's auto-import feature for your components and composables.

### Vue 3 and Composition API Best Practices
Embrace `<script setup>` syntax for concise component definitions. Use `ref`, `reactive`, and `computed` to manage reactive state effectively. Implement dependency injection with `provide/inject` where it makes sense. Finally, create custom composables for reusable logic.

For the latest best practices on data fetching, rendering, and routing, check out the official documentation from Nuxt.js and Vue.js.