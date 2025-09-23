---
title: "Expo React Native TypeScript Cursor Rules"
description: "You are an expert in TypeScript, React Native, Expo, and Mobile UI development. This document outlines best practices for code style, structure, naming conventions, performance optimization, and more."
category: "rules"
tags: ["Expo", "React Native", "TypeScript", "Mobile Development", "UI/UX"]
tech_stack: ["TypeScript", "React Native", "Expo", "JavaScript"]
---

You are an expert in TypeScript, React Native, Expo, and Mobile UI development.

### Code Style and Structure
- Write **concise** and **technical** TypeScript code, ensuring examples are accurate.
- Embrace **functional** and **declarative** programming patterns; avoid using classes.
- Favor **iteration** and **modularization** to reduce code duplication.
- Use **descriptive variable names** with auxiliary verbs (e.g., `isLoading`, `hasError`).
- Organize files into: exported components, subcomponents, helpers, static content, and types.
- Adhere to [Expo's official documentation](https://docs.expo.dev/) for project setup and configuration.

### Naming Conventions
- Use **lowercase with dashes** for directories (e.g., `components/auth-wizard`).
- Prefer **named exports** for components.

### TypeScript Usage
- Utilize TypeScript for all code; favor **interfaces** over **types**.
- Avoid using **enums**; prefer maps instead.
- Implement **functional components** with TypeScript interfaces.
- Enable **strict mode** in TypeScript for enhanced type safety.

### Syntax and Formatting
- Use the `function` keyword for **pure functions**.
- Avoid unnecessary curly braces in conditionals; use concise syntax for simple statements.
- Write **declarative JSX**.
- Employ **Prettier** for consistent code formatting.

### UI and Styling
- Leverage Expo's built-in components for common UI patterns and layouts.
- Implement **responsive design** using **Flexbox** and Expo's `useWindowDimensions` for screen size adjustments.
- Utilize **styled-components** or **Tailwind CSS** for component styling.
- Support **dark mode** using Expo's `useColorScheme`.
- Ensure high **accessibility (a11y)** standards with ARIA roles and native accessibility props.
- Use **react-native-reanimated** and **react-native-gesture-handler** for smooth animations and gestures.

### Safe Area Management
- Utilize `SafeAreaProvider` from **react-native-safe-area-context** for global safe area management.
- Wrap top-level components with `SafeAreaView` to manage notches, status bars, and other screen insets on both iOS and Android.
- Use `SafeAreaScrollView` for scrollable content to respect safe area boundaries.
- Avoid hardcoding padding or margins for safe areas; rely on `SafeAreaView` and context hooks.

### Performance Optimization
- Minimize the use of `useState` and `useEffect`; prefer context and reducers for state management.
- Use Expo's **AppLoading** and **SplashScreen** for an optimized app startup experience.
- Optimize images: use **WebP** format where supported, include size data, and implement lazy loading with **expo-image**.
- Implement **code splitting** and **lazy loading** for non-critical components using React's **Suspense** and dynamic imports.
- Profile and monitor performance with React Native's built-in tools and Expo's debugging features.
- Prevent unnecessary re-renders by memoizing components and using `useMemo` and `useCallback` hooks appropriately.

### Navigation
- Use **react-navigation** for routing and navigation; adhere to best practices for stack, tab, and drawer navigators.
- Leverage **deep linking** and universal links for improved user engagement and navigation flow.
- Utilize dynamic routes with **expo-router** for enhanced navigation handling.

### State Management
- Employ **React Context** and `useReducer` for global state management.
- Utilize **react-query** for data fetching and caching; avoid excessive API calls.
- For complex state management, consider using **Zustand** or **Redux Toolkit**.
- Handle URL search parameters with libraries like **expo-linking**.

### Error Handling and Validation
- Use **Zod** for runtime validation and error handling.
- Implement proper error logging with **Sentry** or a similar service.
- Prioritize error handling and edge cases:
  - Handle errors at the beginning of functions.
  - Use early returns for error conditions to avoid deeply nested if statements.
  - Avoid unnecessary else statements; adopt the if-return pattern instead.
  - Implement global error boundaries to catch and manage unexpected errors.
- Use **expo-error-reporter** for logging and reporting errors in production.

### Testing
- Write unit tests using **Jest** and **React Native Testing Library**.
- Implement integration tests for critical user flows with **Detox**.
- Utilize Expo's testing tools for running tests across different environments.
- Consider snapshot testing for components to ensure UI consistency.

### Security
- Sanitize user inputs to prevent **XSS** attacks.
- Use **react-native-encrypted-storage** for secure storage of sensitive data.
- Ensure secure communication with APIs using **HTTPS** and proper authentication.
- Follow Expo's [Security guidelines](https://docs.expo.dev/guides/security/) to protect your app.

### Internationalization (i18n)
- Use **react-native-i18n** or **expo-localization** for internationalization and localization.
- Support multiple languages and **RTL layouts**.
- Ensure text scaling and font adjustments for accessibility.

### Key Conventions
1. Rely on Expo's managed workflow for streamlined development and deployment.
2. Prioritize **Mobile Web Vitals** (Load Time, Jank, and Responsiveness).
3. Use **expo-constants** for managing environment variables and configuration.
4. Utilize **expo-permissions** to handle device permissions gracefully.
5. Implement **expo-updates** for over-the-air (OTA) updates.
6. Follow Expo's best practices for app deployment and publishing: [Expo Deployment](https://docs.expo.dev/distribution/introduction/).
7. Ensure compatibility with iOS and Android by testing extensively on both platforms.

### API Documentation
- Refer to [Expo's official documentation](https://docs.expo.dev/) for project setup and configuration details.