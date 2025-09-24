---
title: "Expo React Native TypeScript Cursor Rules"
description: "You are an expert in TypeScript, React Native, Expo, and Mobile UI development. This document outlines best practices for code style, structure, naming conventions, performance optimization, and more."
category: "rules"
tags: ["Expo", "React Native", "TypeScript", "Mobile Development", "UI/UX"]
tech_stack: ["TypeScript", "React Native", "Expo", "JavaScript"]
---

You have a solid foundation in TypeScript, React Native, Expo, and mobile UI development. Let’s dive into some best practices and guidelines to keep your code clean and effective.

### Code Style and Structure
Start by writing clear and precise TypeScript code. Make sure your examples are correct. Focus on functional and declarative programming patterns and steer clear of classes. Aim for modularization and iteration to cut down on code duplication. When naming variables, choose descriptive names that include auxiliary verbs, such as `isLoading` or `hasError`. Organize your files into categories like exported components, subcomponents, helpers, static content, and types. Remember to follow [Expo's official documentation](https://docs.expo.dev/) for project setup and configuration.

### Naming Conventions
For directory names, stick to lowercase letters and use dashes, like `components/auth-wizard`. When exporting components, prefer named exports.

### TypeScript Usage
Make TypeScript your go-to for all code. Use interfaces more than types, and skip enums in favor of maps. Implement functional components with TypeScript interfaces, and don’t forget to enable strict mode for better type safety.

### Syntax and Formatting
When writing pure functions, use the `function` keyword. Keep your code tidy by avoiding unnecessary curly braces in conditionals and opting for concise syntax. Write declarative JSX and use Prettier to maintain consistent formatting throughout your code.

### UI and Styling
Take advantage of Expo's built-in components for common UI patterns and layouts. Use Flexbox and Expo's `useWindowDimensions` to create responsive designs. You can choose styled-components or Tailwind CSS for component styling. Don’t forget to support dark mode by using Expo's `useColorScheme`. Ensure your app meets high accessibility standards by incorporating ARIA roles and native accessibility props. For smooth animations and gestures, utilize `react-native-reanimated` and `react-native-gesture-handler`.

### Safe Area Management
Incorporate `SafeAreaProvider` from **react-native-safe-area-context** for global safe area management. Wrap your top-level components with `SafeAreaView` to accommodate notches, status bars, and other screen insets on both iOS and Android. For scrollable content, use `SafeAreaScrollView` to respect safe area boundaries. Avoid hardcoding padding or margins; rely on `SafeAreaView` and context hooks instead.

### Performance Optimization
Minimize the use of `useState` and `useEffect`. Instead, consider using context and reducers for state management. Use Expo's **AppLoading** and **SplashScreen** to optimize your app startup experience. Optimize images by using the **WebP** format where possible, including size data, and implementing lazy loading with **expo-image**. Break your code into chunks and use lazy loading for non-critical components with React's **Suspense** and dynamic imports. Monitor your app's performance with React Native's built-in tools and Expo's debugging features. Prevent unnecessary re-renders by memoizing components and using `useMemo` and `useCallback` hooks effectively.

### Navigation
For routing and navigation, use **react-navigation** and follow best practices for stack, tab, and drawer navigators. Improve user engagement through deep linking and universal links. Use dynamic routes with **expo-router** for better navigation handling.

### State Management
For global state management, utilize **React Context** and `useReducer`. Use **react-query** for data fetching and caching, and limit excessive API calls. If you face complex state management tasks, consider **Zustand** or **Redux Toolkit**. Handle URL search parameters with libraries like **expo-linking**.

### Error Handling and Validation
Employ **Zod** for runtime validation and error handling. Make sure to log errors properly using **Sentry** or similar services. Focus on handling errors and edge cases early on:
- Catch errors at the start of functions.
- Use early returns to tackle error conditions and avoid deeply nested if statements.
- Skip unnecessary else statements by adopting the if-return pattern.
- Implement global error boundaries to manage unexpected errors.
- Use **expo-error-reporter** for logging and reporting errors in production.

### Testing
Write unit tests using **Jest** and **React Native Testing Library**. For critical user flows, implement integration tests with **Detox**. Leverage Expo's testing tools to run tests across different environments. Don’t forget about snapshot testing to ensure UI consistency.

### Security
Make sure to sanitize user inputs to guard against **XSS** attacks. Use **react-native-encrypted-storage** for securely storing sensitive data. Ensure secure communication with APIs by using **HTTPS** and proper authentication. Follow Expo's [Security guidelines](https://docs.expo.dev/guides/security/) to keep your app safe.

### Internationalization (i18n)
Use **react-native-i18n** or **expo-localization** for internationalization and localization. Support multiple languages and accommodate **RTL layouts**. Adjust text scaling and fonts to enhance accessibility.

### Key Conventions
1. Rely on Expo's managed workflow for smoother development and deployment.
2. Keep an eye on **Mobile Web Vitals** like Load Time, Jank, and Responsiveness.
3. Use **expo-constants** to manage environment variables and configuration.
4. Handle device permissions gracefully with **expo-permissions**.
5. Implement **expo-updates** for over-the-air (OTA) updates.
6. Check out Expo's best practices for app deployment and publishing: [Expo Deployment](https://docs.expo.dev/distribution/introduction/).
7. Test extensively on both iOS and Android to ensure compatibility.

### API Documentation
For detailed information on project setup and configuration, refer to [Expo's official documentation](https://docs.expo.dev/).