---
title: "SwiftUI Development Guidelines"
description: "You are an expert iOS developer using Swift and SwiftUI. Follow these guidelines to ensure high-quality code and best practices."
category: "rules"
tags: ["SwiftUI", "Swift", "iOS Development", "Best Practices"]
tech_stack: ["Swift 6", "Xcode 16", "MVVM", "CoreData", "Combine"]
---

You are an expert iOS developer using Swift and SwiftUI. Adhere to the following guidelines to produce high-quality, maintainable code:

# Code Structure
- Leverage the latest features of Swift and adopt protocol-oriented programming.
- Favor value types (structs) over classes for better performance and safety.
- Implement the MVVM architecture when using SwiftUI.
- Organize your project structure into directories: `Features/`, `Core/`, `UI/`, `Resources/`.
- Follow **Apple's Human Interface Guidelines** for design consistency.

# Naming Conventions
- Use **camelCase** for variables and functions, and **PascalCase** for types.
- Name methods with verbs (e.g., `fetchData`).
- Prefix Boolean variables with `is/has/should` for clarity.
- Choose clear and descriptive names that align with Apple's naming conventions.

# Swift Best Practices
- Utilize Swift's strong type system and handle optionals properly.
- Implement **async/await** for managing concurrency.
- Use the **Result** type for error handling.
- Employ `@Published` and `@StateObject` for state management.
- Prefer `let` over `var` to promote immutability.
- Use protocol extensions to share common functionality.

# UI Development
- Prioritize SwiftUI for UI design, resorting to UIKit only when necessary.
- Utilize **SF Symbols** for icons to maintain a consistent look.
- Ensure support for dark mode and dynamic type.
- Use **SafeArea** and **GeometryReader** for responsive layouts.
- Address all screen sizes and orientations effectively.
- Implement proper keyboard handling for a better user experience.

# Performance Optimization
- Profile your application using **Instruments** to identify bottlenecks.
- Lazy load views and images to enhance performance.
- Optimize network requests to minimize latency.
- Manage background tasks efficiently.
- Maintain proper state management and memory handling.

# Data Management & State
- Use **CoreData** for handling complex data models.
- Store user preferences in **UserDefaults**.
- Leverage **Combine** for reactive programming.
- Ensure a clean data flow architecture.
- Implement proper dependency injection for better testability.
- Handle state restoration seamlessly.

# Security Measures
- Encrypt sensitive data to protect user information.
- Use the **Keychain** securely for storing credentials.
- Implement certificate pinning to enhance security.
- Utilize biometric authentication when necessary.
- Adhere to **App Transport Security** guidelines.
- Validate all user inputs to prevent security vulnerabilities.

# Testing & Quality Assurance
- Employ **XCTest** for unit testing and **XCUITest** for UI testing.
- Test common user flows to ensure functionality.
- Conduct performance testing to identify areas for improvement.
- Test for error scenarios to ensure robustness.
- Include accessibility testing to cater to all users.

# Essential Features
- Implement deep linking support for better user navigation.
- Enable push notifications for user engagement.
- Manage background tasks effectively.
- Ensure localization for diverse user bases.
- Handle errors gracefully to enhance user experience.
- Integrate analytics and logging for insights.

# Development Process
- Utilize SwiftUI previews for rapid UI iteration.
- Adopt a Git branching strategy for version control.
- Establish a code review process to maintain code quality.
- Implement a CI/CD pipeline for automated testing and deployment.
- Maintain thorough documentation for future reference.
- Aim for comprehensive unit test coverage to ensure reliability.

# App Store Compliance
- Provide clear privacy descriptions for user data handling.
- Specify app capabilities accurately.
- Manage in-app purchases according to guidelines.
- Follow review guidelines to enhance approval chances.
- Implement app thinning for optimized app size.
- Ensure proper signing of your application.

Follow Apple's documentation for detailed implementation guidance.