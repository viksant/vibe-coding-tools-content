---
title: React Performance Rules
description: Performance optimization rules for React applications
author: viksant
date: "2025-09-21"
tags:
  - performance
  - react
  - optimization
tech_stack:
  - react
  - typescript
  - webpack
category: rules
subcategory: general
---

# React Performance Rules

## Component Optimization
- Use React.memo for expensive components
- Implement proper key props for lists
- Avoid inline functions in render

## State Management
- Use useCallback for event handlers
- Implement useMemo for expensive calculations
- Keep state close to where it's used

## Bundle Optimization
- Implement code splitting with React.lazy
- Use dynamic imports for large dependencies