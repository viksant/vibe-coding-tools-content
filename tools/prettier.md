---
title: "Prettier"
description: "An opinionated code formatter that enforces consistent style across your codebase, eliminating debates about code formatting and integrating seamlessly with most editors."
category: "tools"
tags: ["code-formatting", "style-guide", "consistency", "automation", "pre-commit", "linting"]
tech_stack: ["javascript", "typescript", "css", "html", "json", "markdown", "yaml"]
---

### Tool Benefits
**Prettier** ensures that all code in a project adheres to a consistent style, which improves readability and maintainability. Key benefits include:
- **Eliminates debates**: Reduces discussions about code style by enforcing a single standard.
- **Wide language support**: Works with JavaScript, TypeScript, CSS, HTML, JSON, Markdown, and YAML.
- **Editor integration**: Easily integrates with popular editors like VSCode, Atom, and Sublime Text.
- **Automated formatting**: Can be configured to format code automatically on save or during pre-commit hooks.

### Setup & Installation
To install Prettier, follow these steps based on your environment:

#### Node.js Environment
1. Ensure you have Node.js installed. Check with:
   ```bash
   node -v
   ```
2. Install Prettier globally:
   ```bash
   npm install --global prettier
   ```
3. Alternatively, install it locally in your project:
   ```bash
   npm install --save-dev prettier
   ```

#### Editor Integration
- **VSCode**: Install the Prettier extension from the marketplace.
- **Atom**: Install the `prettier-atom` package.
- **Sublime Text**: Use the `Prettier` package via Package Control.

### Configuration
Create a `.prettierrc` file in your project root to customize Prettier settings. Here are some essential options:
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
- Use **single quotes** for strings to maintain consistency.
- Set **trailing commas** to `es5` for cleaner diffs.

### Usage Guide
To format a file, run:
```bash
prettier --write path/to/your/file.js
```
To format all files in a directory:
```bash
prettier --write "**/*.js"
```
To check formatting without making changes:
```bash
prettier --check path/to/your/file.js
```

### Advanced Features
- **Pre-commit hooks**: Use `husky` to run Prettier before commits:
  1. Install `husky`:
     ```bash
     npm install --save-dev husky
     ```
  2. Add a hook in `package.json`:
     ```json
     "husky": {
       "hooks": {
         "pre-commit": "prettier --write ."
       }
     }
     ```
- **Integration with ESLint**: Combine Prettier with ESLint to handle both formatting and linting:
  1. Install necessary packages:
     ```bash
     npm install --save-dev eslint eslint-config-prettier eslint-plugin-prettier
     ```
  2. Update `.eslintrc`:
     ```json
     {
       "extends": ["plugin:prettier/recommended"]
     }
     ```

### Troubleshooting
- **Prettier not formatting on save**: Check your editor settings to ensure format on save is enabled.
- **Conflicting ESLint rules**: Ensure that `eslint-config-prettier` is included to disable conflicting rules.
- **File types not recognized**: Verify that the file extension is supported by Prettier.

### Best Practices
- **Consistent configuration**: Use a shared `.prettierrc` file across your team to maintain consistency.
- **Run Prettier in CI**: Integrate Prettier checks in your Continuous Integration pipeline to enforce style rules.
- **Use editor plugins**: Leverage editor integrations to format code automatically on save, enhancing developer experience.