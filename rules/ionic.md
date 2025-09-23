---
title: "Ionic Cursor Guidelines"
description: "You are an expert in Ionic and Cordova, specializing in TypeScript and Angular for mobile and web application development. This document outlines best practices for project structure, file naming, and coding conventions."
category: "rules"
tags: ["ionic", "cordova", "angular", "typescript"]
tech_stack: ["Ionic", "Cordova", "TypeScript", "Angular"]
---

You are an expert in Ionic and Cordova, specializing in TypeScript and Angular for mobile and web application development. This document outlines best practices for project structure, file naming, and coding conventions.

### Project Structure and File Naming
- Organize files into feature-specific directories, such as `services/`, `components/`, and `pipes/`.
- Utilize environment variables to manage different deployment stages: development, staging, and production.
- Develop build scripts to facilitate the bundling and deployment processes.
- Implement a Continuous Integration/Continuous Deployment (CI/CD) pipeline for streamlined updates.
- Establish staging and canary environments for testing new features safely.

### Project Structure and Organization
- Use clear and descriptive names for variables and functions, such as `getUsers()` and `calculateTotalPrice()`.
- Keep classes concise and focused on a single responsibility.
- Minimize the use of global state to enhance maintainability.
- Manage routing through a dedicated module to improve organization.
- Leverage the latest ES6+ features and best practices in TypeScript and Angular.
- Centralize API calls and error handling within services to promote reusability.
- Handle all storage operations through a single point of entry, ensuring that storage keys are easily accessible and manageable.

### Naming Conventions
- Use **camelCase** for function and variable names (e.g., `fetchData`, `updateProfile`).
- Ensure consistency in naming across the codebase to improve readability and maintainability.