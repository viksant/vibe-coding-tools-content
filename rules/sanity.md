---
title: "Best Practices for Sanity Development"
description: "Comprehensive guidelines for effective Sanity schema design and integration."
category: "rules"
tags: ["sanity", "cms", "headless", "typescript", "groq"]
tech_stack: ["Sanity", "TypeScript", "GROQ", "Next.js"]
---

You’re diving into the world of Sanity, TypeScript, and GROQ query optimization. Let’s go through some essential guidelines to help you navigate your development process smoothly.

# Sanity Development Guidelines

## Sanity Schema Rules

### 1. Choose Descriptive Schema Names

For clarity, use names that describe the purpose of your schemas. Here’s an example:

```javascript
export default {
  name: 'blogPost',
  title: 'Blog Post',
  type: 'document'
}
```

Clear names make your code easier to read and maintain.

### 2. Always Add Descriptions

Descriptions are key for:

- Complex fields
- Fields with specific validation rules
- Fields that impact other parts of your system

Adding descriptions helps everyone understand what each field does and what limitations it has.

### 3. Set Up Validation Rules

Be sure to validate your fields. Check for:

- Required fields
- String lengths
- Number ranges
- Custom business logic

Here’s how you might set up validation:

```javascript
{
  name: 'title',
  title: 'Title',
  type: 'string',
  validation: Rule => Rule.required().max(80)
}
```

### 4. Organize with Fieldsets

Grouping related fields can improve clarity. Here’s an example of how to do that:

```javascript
fieldsets: [
  {
    name: 'social',
    title: 'Social Media',
    options: { collapsible: true, collapsed: true }
  }
]
```

### 5. Keep Icon Usage Consistent

Use icons from `@sanity/icons` or `react-icons` consistently across your schemas to maintain a uniform look.

## TypeScript Integration

### 1. Generate Types Automatically

Tools like `sanity-codegen` can help you automatically create TypeScript types from your schemas. This step is crucial for ensuring type safety.

### 2. Type Your Queries

Here’s a way to define the types for your queries:

```typescript
import { SanityDocument } from '@sanity/client'

interface BlogPost extends SanityDocument {
  title: string
  slug: { current: string }
  content: PortableTextBlock[]
}
```

## GROQ Query Best Practices

### 1. Use Projections Wisely

To boost performance, only fetch the fields you actually need. Here’s an example:

```groq
*[_type == "blogPost"] {
  _id,
  title,
  slug,
  "author": author->name
}
```

### 2. Handle References Correctly

Make sure to use the arrow operator when working with references:

```groq
*[_type == "blogPost"] {
  ...,
  "authorName": author->name,
  "categoryTitles": categories[]->title
}
```

### 3. Implement Pagination Properly

To manage large datasets, use pagination. Here’s a simple example:

```groq
*[_type == "blogPost"] | order(_createdAt desc) [0...10]
```

## Performance Optimization

### 1. Use CDN URLs for Images

Always take advantage of Sanity's image CDN and apply any necessary transformations to optimize loading times.

### 2. Set Up Caching Strategies

Consider these options:

- Use Incremental Static Regeneration (ISR) with Next.js.
- Set appropriate cache headers.
- Utilize Sanity's webhook for on-demand revalidation.

### 3. Optimize Bundle Size

To improve load times, try these techniques:

- Lazy load components in Sanity Studio.
- Use dynamic imports for larger preview components to reduce initial load time.

By following these guidelines, you’ll be well on your way to creating a well-structured and efficient application using Sanity, TypeScript, and GROQ. Happy coding!