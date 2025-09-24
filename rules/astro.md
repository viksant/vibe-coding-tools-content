---
title: "Astro Cursor Rules"
description: "You are an expert in JavaScript, TypeScript, and the Astro framework for scalable web development. This document outlines key principles and best practices for effective Astro development."
category: "rules"
tags: ["Astro", "JavaScript", "TypeScript", "Tailwind CSS", "Web Development"]
tech_stack: ["astro", "tailwind"]
---

You have a solid foundation in JavaScript, TypeScript, and the Astro framework, making you well-equipped for scalable web development. Let’s break down some key principles and structures you should keep in mind.

### Key Principles
First, aim for clarity and technical accuracy when responding to questions. Use examples from Astro to illustrate your points. Focus on leveraging Astro's partial hydration and support for multiple frameworks. It’s wise to prioritize static generation and keep JavaScript usage low to boost performance. Remember to use descriptive variable names and stick to Astro's naming conventions. Lastly, organize your files according to Astro's file-based routing system for better structure.

### Astro Project Structure
Follow the recommended project setup to keep things tidy:
```
src/
  components/
  layouts/
  pages/
  styles/
public/
astro.config.mjs
```

### Component Development
When creating components, use `.astro` files. Don’t hesitate to incorporate framework-specific components like React, Vue, or Svelte. Focus on proper component composition and reusability. Use Astro's component props to pass data around, and make sure to leverage built-in components like `<Markdown />` when it fits.

### Routing and Pages
Utilize Astro's file-based routing in the `src/pages/` directory. You can create dynamic routes using the `[...slug].astro` syntax. To generate static pages with dynamic routes, implement `getStaticPaths()`. Make sure to handle 404 errors properly by creating a `404.astro` page.

### Content Management
For content-rich pages, opt for Markdown (.md) or MDX (.mdx) files. Take advantage of Astro's built-in support for frontmatter in these files. Organizing your content into content collections can simplify management.

### Styling
Use scoped styling with `<style>` tags in your `.astro` files. Import global styles in layouts as needed. If you prefer, you can also use CSS preprocessing with Sass or Less. Don't forget to implement responsive design using CSS custom properties and media queries.

### Performance Optimization
Keep client-side JavaScript to a minimum by leveraging Astro's static generation. Use the `client:*` directives wisely for partial hydration:
- `client:load` for immediate interactivity 
- `client:idle` for non-critical interactions 
- `client:visible` for components that should load when visible

Implement lazy loading for images and other assets, and use Astro's built-in asset optimization features to enhance performance.

### Data Fetching
Pass data to components using `Astro.props`. Use `getStaticPaths()` for data fetching during the build process, and `Astro.glob()` for efficient local file handling. Ensure you handle errors properly during data fetching.

### SEO and Meta Tags
Add meta information using Astro's `<head>` tag. Implement canonical URLs for better SEO, and use the `<SEO>` component pattern for reusable SEO setups.

### Integrations and Plugins
Astro integrations can extend functionality, such as `@astrojs/image`. Make sure to configure these integrations correctly in `astro.config.mjs`, and favor official Astro integrations for compatibility.

### Build and Deployment
Optimize your build process using Astro's build command. Manage environment variables for different contexts, and choose static hosting platforms compatible with Astro, like Netlify or Vercel. Setting up CI/CD pipelines can help automate builds and deployments.

### Styling with Tailwind CSS
Integrate Tailwind CSS into your project using `@astrojs/tailwind`.

### Tailwind CSS Best Practices
Utilize Tailwind's utility classes extensively in your Astro components. Use responsive design utilities like `sm:`, `md:`, and `lg:` for different screen sizes. Stick to Tailwind's color palette and spacing scale for a consistent look. If needed, you can implement custom theme extensions in `tailwind.config.cjs`, but avoid using the `@apply` directive.

### Testing
Incorporate unit tests for utility functions and helpers. For testing the entire site, consider using end-to-end tools like Cypress. If it fits your project, visual regression testing can also be beneficial.

### Accessibility
Ensure your Astro components have a proper semantic HTML structure. Implement ARIA attributes where necessary and support keyboard navigation for interactive elements.

### Key Conventions
1. Stick to Astro's Style Guide for consistent formatting.
2. Use TypeScript to enhance type safety and improve the developer experience.
3. Implement proper error handling and logging.
4. Leverage Astro's RSS feed generation for content-heavy sites.
5. Use Astro's Image component for optimized image delivery.

### Performance Metrics
Keep an eye on Core Web Vitals (LCP, FID, CLS) throughout development. Tools like Lighthouse and WebPageTest can help with performance auditing. Establish performance budgets and monitoring practices to ensure your site remains fast.

For more detailed information about components, routing, and integrations, check out Astro's official documentation.