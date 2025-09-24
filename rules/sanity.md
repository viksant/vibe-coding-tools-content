---
title: "Best Practices for Sanity Development"
description: "Comprehensive guidelines for effective Sanity schema design and integration."
category: "rules"
tags: ["sanity", "cms", "headless", "typescript", "groq"]
tech_stack: ["Sanity", "TypeScript", "GROQ", "Next.js"]
---

You are an expert in Sanity, TypeScript, and GROQ query optimization...

# Sanity Development Guidelines

## Sanity Schema Rules

### 1. Use Descriptive Schema Names

**Example:**
```javascript
export default {
  name: 'blogPost',
  title: 'Blog Post',
  type: 'document'
}
```
Utilizing clear and descriptive names enhances readability and maintainability.

### 2. Always Include Descriptions

**Essential for:**
- Complex fields
- Fields with specific validation rules
- Fields that influence other components of the system

Providing descriptions aids in understanding the purpose and constraints of each field.

### 3. Validation Rules

Ensure validation for:
- Required fields
- String lengths
- Number ranges
- Custom business logic validations

**Example:**
```javascript
{
  name: 'title',
  title: 'Title',
  type: 'string',
  validation: Rule => Rule.required().max(80)
}
```

### 4. Use Fieldsets for Organization

Group related fields to improve clarity:

**Example:**
```javascript
fieldsets: [
  {
    name: 'social',
    title: 'Social Media',
    options: { collapsible: true, collapsed: true }
  }
]
```

### 5. Consistent Icon Usage

Utilize icons from `@sanity/icons` or `react-icons` uniformly throughout your schemas.

## TypeScript Integration

### 1. Always Generate Types

Utilize tools like `sanity-codegen` to automatically generate TypeScript types from your schemas, ensuring type safety.

### 2. Type Your Queries

**Example:**
```typescript
import { SanityDocument } from '@sanity/client'

interface BlogPost extends SanityDocument {
  title: string
  slug: { current: string }
  content: PortableTextBlock[]
}
```

## GROQ Query Best Practices

### 1. Use Projections Efficiently

Fetch only the necessary fields to optimize performance:

**Example:**
```groq
*[_type == "blogPost"] {
  _id,
  title,
  slug,
  "author": author->name
}
```

### 2. Handle References Properly

Always utilize the arrow operator for references:

**Example:**
```groq
*[_type == "blogPost"] {
  ...,
  "authorName": author->name,
  "categoryTitles": categories[]->title
}
```

### 3. Implement Proper Pagination

**Example:**
```groq
*[_type == "blogPost"] | order(_createdAt desc) [0...10]
```

## Performance Optimization

### 1. Use CDN URLs for Images

Always leverage Sanity's image CDN, applying necessary transformations for optimal loading.

### 2. Implement Caching Strategies

- Utilize Incremental Static Regeneration (ISR) with Next.js.
- Set appropriate cache headers.
- Employ Sanity's webhook for on-demand revalidation.

### 3. Optimize Bundle Size

- Lazy load Sanity Studio components.
- Use dynamic imports for larger preview components to reduce initial load time.