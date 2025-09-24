---
title: "Flutter + Riverpod & Supabase Coding Guidelines"
description: "You are an expert in Flutter, Dart, Riverpod, Freezed, Flutter Hooks, and Supabase. This document outlines key principles and best practices for writing clean, efficient Dart code."
category: "rules"
tags: ["Flutter", "Dart", "Riverpod", "Supabase", "Best Practices"]
tech_stack: ["Riverpod", "Freezed", "Flutter Hooks", "Supabase"]
---

You have a solid grasp of Flutter, Dart, Riverpod, Freezed, Flutter Hooks, and Supabase. Let’s dive into some important principles and best practices to enhance your development experience.

## Key Principles
First off, aim for clear and concise Dart code. This means using accurate examples that speak for themselves. When writing code, lean towards functional and declarative patterns when possible. Focus on composition instead of inheritance to boost flexibility in your projects. Also, be sure to use descriptive variable names that include auxiliary verbs, like `isLoading` or `hasError`, to make your code more readable. Finally, keep your files organized. Structure them by exported widgets, subwidgets, helpers, static content, and types.

## Dart/Flutter Best Practices
Let’s talk about best practices. Start by using **const constructors** for immutable widgets. This choice can greatly improve performance. When you need to create immutable state classes and unions, Freezed is your go-to tool. For function definitions, the arrow syntax can help keep things concise. Use expression bodies for your single-line getters and setters. And don't forget to add trailing commas; they can make your code cleaner and help with better version control diffs.

## Error Handling and Validation
Next, consider error handling in your views. Instead of SnackBars, use `SelectableText.rich` to show errors. Highlight errors in red to ensure they stand out. It's also crucial to manage empty states effectively on your screens. Use **AsyncValue** for a thorough approach to handling errors and tracking loading states.

## Riverpod-Specific Guidelines
When working with Riverpod, use the `@riverpod` annotation to generate your providers. Look towards **AsyncNotifierProvider** and **NotifierProvider** instead of **StateProvider**. It's best to steer clear of **StateProvider**, **StateNotifierProvider**, and **ChangeNotifierProvider**. Don’t forget to utilize `ref.invalidate()` to manually trigger updates to your providers. Also, make sure to cancel asynchronous operations properly when disposing of widgets.

## Performance Optimization
To keep your app running smoothly, employ **const widgets** whenever you can to cut down on unnecessary rebuilds. For lists, consider using `ListView.builder` for better performance. Use **AssetImage** for static images and **cached_network_image** for images fetched from the web. Lastly, ensure you handle errors properly for Supabase operations, especially regarding network issues.

## Key Conventions
Here are some conventions to keep in mind. Use **GoRouter** or **auto_route** for navigation and deep linking. Pay attention to Flutter performance metrics, like the time it takes for the first meaningful paint and when the app becomes interactive. Favor **stateless widgets**: leverage **ConsumerWidget** with Riverpod for widgets that rely on state, and opt for **HookConsumerWidget** when using Riverpod with Flutter Hooks.

## UI and Styling
For UI and styling, take advantage of Flutter's built-in widgets while also crafting your custom widgets. Implement responsive design using `LayoutBuilder` or `MediaQuery`. Consistent styling across your application is key—make use of themes. When accessing theme properties, use `Theme.of(context).textTheme.titleLarge` instead of `headline6` and `headlineSmall` instead of `headline5`, and so on.

## Model and Database Conventions
In your database tables, remember to include `createdAt`, `updatedAt`, and `isDeleted` fields. When it comes to model serialization, leverage `@JsonSerializable(fieldRename: FieldRename.snake)`. For read-only fields, apply `@JsonKey(includeFromJson: true, includeToJson: false)`.

## Widgets and UI Components
For widget creation, opt for small, private widget classes instead of methods like `Widget _build...`. Use **RefreshIndicator** to add pull-to-refresh functionality. When dealing with `TextFields`, set the right properties for `textCapitalization`, `keyboardType`, and `textInputAction`. And always include an **errorBuilder** when using `Image.network`.

## Miscellaneous
For debugging, stick with **log** instead of **print** to keep your output tidy. Consider using **Flutter Hooks** and **Riverpod Hooks** whenever relevant. Keep your lines to a maximum of 80 characters, and add commas before closing brackets for functions with multiple parameters. For enums stored in the database, use `@JsonValue(int)`.

## Code Generation
When it comes to code generation, utilize **build_runner** for generating code from annotations like Freezed, Riverpod, and JSON serialization. After modifying annotated classes, run `flutter pub run build_runner build --delete-conflicting-outputs` to ensure everything is up-to-date.

## Documentation
Finally, document complex logic and any non-obvious decisions thoroughly. Always refer to the official documentation for Flutter, Riverpod, and Supabase to stay aligned with best practices. 

By following these guidelines, you’ll enhance your Flutter development process and create more maintainable, efficient applications.