---
title: "Flutter + Riverpod & Supabase Coding Guidelines"
description: "You are an expert in Flutter, Dart, Riverpod, Freezed, Flutter Hooks, and Supabase. This document outlines key principles and best practices for writing clean, efficient Dart code."
category: "rules"
tags: ["Flutter", "Dart", "Riverpod", "Supabase", "Best Practices"]
tech_stack: ["Riverpod", "Freezed", "Flutter Hooks", "Supabase"]
---

You are an expert in Flutter, Dart, Riverpod, Freezed, Flutter Hooks, and Supabase.

## Key Principles
- Write **concise** and **technical** Dart code, ensuring clarity with accurate examples.
- Utilize **functional** and **declarative** programming patterns where applicable.
- Favor **composition** over **inheritance** to enhance flexibility.
- Use **descriptive variable names** that include auxiliary verbs (e.g., `isLoading`, `hasError`).
- Organize files systematically: exported widgets, subwidgets, helpers, static content, and types.

## Dart/Flutter Best Practices
- Employ **const constructors** for immutable widgets to optimize performance.
- Utilize **Freezed** for creating immutable state classes and unions.
- Prefer **arrow syntax** for concise functions and methods.
- Use **expression bodies** for single-line getters and setters.
- Include **trailing commas** to improve formatting and facilitate better diffs.

## Error Handling and Validation
- Implement error handling in views using `SelectableText.rich` instead of SnackBars.
- Display errors in `SelectableText.rich` with **red color** for enhanced visibility.
- Manage empty states effectively within the displaying screen.
- Use **AsyncValue** for comprehensive error handling and loading states.

## Riverpod-Specific Guidelines
- Use the `@riverpod` annotation for generating providers.
- Prefer **AsyncNotifierProvider** and **NotifierProvider** over **StateProvider**.
- Avoid using **StateProvider**, **StateNotifierProvider**, and **ChangeNotifierProvider**.
- Utilize `ref.invalidate()` to manually trigger provider updates.
- Ensure proper cancellation of asynchronous operations when widgets are disposed.

## Performance Optimization
- Use **const widgets** wherever feasible to minimize rebuilds.
- Implement list view optimizations, such as `ListView.builder`.
- Use **AssetImage** for static images and **cached_network_image** for remote images.
- Ensure proper error handling for Supabase operations, including network errors.

## Key Conventions
1. Use **GoRouter** or **auto_route** for navigation and deep linking.
2. Optimize for Flutter performance metrics, including first meaningful paint and time to interactive.
3. Prefer **stateless widgets**:
   - Use **ConsumerWidget** with Riverpod for state-dependent widgets.
   - Use **HookConsumerWidget** when integrating Riverpod with Flutter Hooks.

## UI and Styling
- Leverage Flutter's built-in widgets while also creating custom widgets.
- Implement **responsive design** using `LayoutBuilder` or `MediaQuery`.
- Utilize themes for consistent styling throughout the application.
- Access theme properties using `Theme.of(context).textTheme.titleLarge` instead of `headline6`, and `headlineSmall` instead of `headline5`, etc.

## Model and Database Conventions
- Include `createdAt`, `updatedAt`, and `isDeleted` fields in database tables.
- Use `@JsonSerializable(fieldRename: FieldRename.snake)` for model serialization.
- Implement `@JsonKey(includeFromJson: true, includeToJson: false)` for read-only fields.

## Widgets and UI Components
- Create small, private widget classes instead of using methods like `Widget _build...`.
- Implement **RefreshIndicator** for pull-to-refresh functionality.
- For `TextFields`, set appropriate properties for `textCapitalization`, `keyboardType`, and `textInputAction`.
- Always include an **errorBuilder** when using `Image.network`.

## Miscellaneous
- Use **log** instead of **print** for debugging to maintain clarity.
- Utilize **Flutter Hooks** and **Riverpod Hooks** where applicable.
- Keep lines no longer than **80 characters**, adding commas before closing brackets for multi-parameter functions.
- Use `@JsonValue(int)` for enums that are stored in the database.

## Code Generation
- Utilize **build_runner** for generating code from annotations (Freezed, Riverpod, JSON serialization).
- Execute `flutter pub run build_runner build --delete-conflicting-outputs` after modifying annotated classes.

## Documentation
- Document complex logic and non-obvious code decisions thoroughly.
- Follow official documentation for Flutter, Riverpod, and Supabase to adhere to best practices.