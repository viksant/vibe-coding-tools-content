---
title: "Ionic Cursor Guidelines"
description: "You are an expert in Ionic and Cordova, specializing in TypeScript and Angular for mobile and web application development. This document outlines best practices for project structure, file naming, and coding conventions."
category: "rules"
tags: ["ionic", "cordova", "angular", "typescript"]
tech_stack: ["Ionic", "Cordova", "TypeScript", "Angular"]
---

You have a solid background in Ionic and Cordova, focusing on TypeScript and Angular for both mobile and web app development. Let’s explore some practical tips for organizing your projects, naming your files, and sticking to coding conventions.

### Project Structure and File Naming
First off, keep your files organized by grouping them into directories based on their features. For instance, consider using folders like `services/`, `components/`, and `pipes/`. This way, you can quickly locate what you need.

Next, make use of environment variables to manage different stages of deployment, such as development, staging, and production. This approach helps keep things tidy and reduces the chance of errors.

You’ll want to create build scripts to simplify the bundling and deployment processes. This can save you time and effort in the long run. Setting up a Continuous Integration/Continuous Deployment (CI/CD) pipeline also plays a crucial role in ensuring smooth updates.

Don’t forget about staging and canary environments—they let you test new features safely before rolling them out to everyone.

### Project Structure and Organization
Let’s talk about naming. Clear and descriptive names for your variables and functions can make a world of difference. For example, names like `getUsers()` and `calculateTotalPrice()` tell you exactly what each function does.

Keep your classes focused on a single responsibility. This keeps your code clean and makes it easier to manage. Try to minimize the use of global state, as it can complicate maintainability.

Managing routing through a dedicated module can also help improve organization. Plus, leveraging the latest ES6+ features and best practices in TypeScript and Angular will keep your code modern and efficient.

Centralizing API calls and error handling within services promotes reusability. It’s a smart way to ensure your code remains DRY (Don’t Repeat Yourself). Additionally, handle all storage operations through a single point of entry. This setup makes it easier to access and manage storage keys.

### Naming Conventions
When it comes to naming conventions, stick with **camelCase** for your function and variable names. Examples like `fetchData` and `updateProfile` work well here. 

Lastly, consistency in naming throughout your codebase is key. It enhances readability and makes maintenance a breeze. Following these tips will help you create clean, organized, and efficient projects. Happy coding!