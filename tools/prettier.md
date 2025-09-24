---
title: "Prettier"
description: "An opinionated code formatter that enforces consistent style across your codebase, eliminating debates about code formatting and integrating seamlessly with most editors."
category: "tools"
tags: ["code-formatting", "style-guide", "consistency", "automation", "pre-commit", "linting"]
tech_stack: ["javascript", "typescript", "css", "html", "json", "markdown", "yaml"]
---

### Tool Benefits
Prettier keeps your code looking sharp and consistent across your project, which makes it easier to read and maintain. Here’s what you can expect:

- **Cuts down on debates**: It settles discussions about code style by sticking to a single standard.
- **Supports many languages**: You can use it with JavaScript, TypeScript, CSS, HTML, JSON, Markdown, and YAML.
- **Integrates with editors**: It works smoothly with popular editors like VSCode, Atom, and Sublime Text.
- **Automates formatting**: Set it up to format your code automatically when you save or during pre-commit hooks.

### Setup & Installation
Getting Prettier up and running is simple. Here’s how to do it based on your setup:

#### Node.js Environment
1. First, check if you have Node.js installed by running:
   ```bash
   node -v
   ```
2. Install Prettier globally with this command:
   ```bash
   npm install --global prettier
   ```
3. If you prefer to install it locally for your project, use:
   ```bash
   npm install --save-dev prettier
   ```

#### Editor Integration
- **VSCode**: Grab the Prettier extension from the marketplace.
- **Atom**: Install the `prettier-atom` package.
- **Sublime Text**: Use the `Prettier` package via Package Control.

### Configuration
To customize Prettier for your project, create a `.prettierrc` file in the root directory. Here are some helpful options you might want to include:
```json
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5",
  "printWidth": 80
}
```
**Recommended settings**:
- Stick with **single quotes** for strings to keep things uniform.
- Set **trailing commas** to `es5` for cleaner diffs.

### Usage Guide
To format a specific file, run:
```bash
prettier --write path/to/your/file.js
```
Want to format all files in a directory? Just use:
```bash
prettier --write "**/*.js"
```
If you want to check your formatting without making any changes, run:
```bash
prettier --check path/to/your/file.js
```

### Advanced Features
- **Pre-commit hooks**: Use `husky` to run Prettier before you commit your changes:
  1. First, install `husky`:
     ```bash
     npm install --save-dev husky
     ```
  2. Add a hook in your `package.json`:
     ```json
     "husky": {
       "hooks": {
         "pre-commit": "prettier --write ."
       }
     }
     ```
- **ESLint integration**: Pair Prettier with ESLint to manage both formatting and linting:
  1. Install the necessary packages:
     ```bash
     npm install --save-dev eslint eslint-config-prettier eslint-plugin-prettier
     ```
  2. Update your `.eslintrc` file:
     ```json
     {
       "extends": ["plugin:prettier/recommended"]
     }
     ```

### Troubleshooting
If you run into issues, here are some quick fixes:
- **Prettier not formatting on save**: Check your editor settings to make sure format on save is turned on.
- **Conflicting ESLint rules**: Make sure you have `eslint-config-prettier` to disable any conflicting rules.
- **File types not recognized**: Double-check that your file extension is supported by Prettier.

### Best Practices
- **Stay consistent**: Use a shared `.prettierrc` file among your team to keep styles uniform.
- **Run Prettier in CI**: Add Prettier checks to your Continuous Integration pipeline to enforce style rules.
- **Leverage editor plugins**: Use editor integrations to format code automatically on save, which can really enhance the developer experience.