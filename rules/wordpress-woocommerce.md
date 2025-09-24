---
title: "WordPress & WooCommerce Best Practices"
description: "You are an expert in WordPress, WooCommerce, PHP, and related web development technologies. This document outlines key principles for writing effective code."
category: "rules"
tags: ["WordPress", "WooCommerce", "PHP", "Web Development"]
tech_stack: ["WordPress", "WooCommerce", "PHP"]
---

You have a strong grasp of WordPress, WooCommerce, PHP, and other web development technologies. Let’s break down some key principles that can guide your coding practices.

### Key Principles
- Keep your code **concise** and **technical**. Make sure to include clear PHP examples.
- Stick to the **WordPress** and **WooCommerce** coding standards for consistency.
- Use **object-oriented programming** when it makes sense, focusing on **modularity** to keep things organized.
- Choose **iteration** and **modularization** over duplicating code. This keeps your projects clean and manageable.
- Opt for **descriptive** names for your functions, variables, and files. This enhances readability for anyone looking at your code later.
- When naming directories, stick to **lowercase** and separate words with **hyphens**. For example, use paths like `wp-content/themes/my-theme` and `wp-content/plugins/my-plugin`.
- Take advantage of **hooks** (actions and filters) to effectively extend functionality.

### PHP/WordPress/WooCommerce Guidelines
- Make the most of features from **PHP 7.4+** when you can. This includes using typed properties and arrow functions. Here’s a quick example:
  ```php
  class MyClass {
      public function __construct(private string $name) {}
      public function greet(): string {
          return "Hello, {$this->name}!";
      }
  }
  ```
- Follow the **WordPress PHP Coding Standards** to maintain quality and consistency in your work.
- Apply **strict typing** whenever possible. This adds an extra layer of type safety to your code. Here’s how:
  ```php
  declare(strict_types=1);
  function addNumbers(int $a, int $b): int {
      return $a + $b;
  }
  ``` 

By following these guidelines, you'll not only improve your coding skills but also contribute to a better development environment for everyone involved. Happy coding!