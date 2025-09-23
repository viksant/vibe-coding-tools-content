---
title: Production-Ready ESLint Configuration
description: >-
  Comprehensive JavaScript&amp;#x2F;TypeScript linting setup with React,
  accessibility, and Prettier integration for production-ready code quality
author: holabuenastardes6854
date: "2025-09-23"
tags:
  - eslint
  - typescript
  - react
  - linting
tech_stack:
  - ESLint
  - TypeScript
  - React
category: configurations
tool: vscode
---

# Production-Ready ESLint Configuration

## Comprehensive JavaScript/TypeScript Linting Setup

### Installation
```bash
npm install --save-dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin
npm install --save-dev eslint-plugin-react eslint-plugin-react-hooks
npm install --save-dev eslint-plugin-import eslint-plugin-jsx-a11y
npm install --save-dev eslint-config-prettier eslint-plugin-prettier
```

### .eslintrc.js Configuration
```javascript
module.exports = {
  env: {
    browser: true,
    es2021: true,
    node: true,
  },
  extends: [
    'eslint:recommended',
    '@typescript-eslint/recommended',
    'plugin:react/recommended',
    'plugin:react-hooks/recommended',
    'plugin:import/recommended',
    'plugin:jsx-a11y/recommended',
    'prettier',
  ],
  parser: '@typescript-eslint/parser',
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
    ecmaVersion: 'latest',
    sourceType: 'module',
  },
  plugins: [
    'react',
    '@typescript-eslint',
    'import',
    'jsx-a11y',
    'prettier',
  ],
  rules: {
    // TypeScript specific
    '@typescript-eslint/no-unused-vars': 'error',
    '@typescript-eslint/no-explicit-any': 'warn',
    '@typescript-eslint/explicit-function-return-type': 'off',

    // React specific
    'react/react-in-jsx-scope': 'off',
    'react/prop-types': 'off',
    'react-hooks/exhaustive-deps': 'warn',

    // General rules
    'no-console': process.env.NODE_ENV === 'production' ? 'error' : 'warn',
    'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'warn',
    'prefer-const': 'error',
    'no-var': 'error',

    // Import rules
    'import/order': [
      'error',
      {
        groups: [
          'builtin',
          'external',
          'internal',
          'parent',
          'sibling',
          'index',
        ],
        'newlines-between': 'always',
      },
    ],

    // Accessibility
    'jsx-a11y/anchor-is-valid': 'warn',

    // Prettier integration
    'prettier/prettier': 'error',
  },
  settings: {
    react: {
      version: 'detect',
    },
    'import/resolver': {
      typescript: {},
    },
  },
  ignorePatterns: ['dist/', 'build/', 'node_modules/'],
};
```

### .eslintignore
```
node_modules/
dist/
build/
.next/
coverage/
*.d.ts
```

## Usage Scripts
Add to package.json:
```json
{
  "scripts": {
    "lint": "eslint . --ext .js,.jsx,.ts,.tsx",
    "lint:fix": "eslint . --ext .js,.jsx,.ts,.tsx --fix"
  }
}
```