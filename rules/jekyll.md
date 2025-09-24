---
title: "Jekyll Cursor Rules"
description: "You are an expert in Jekyll, Ruby, Tailwind CSS, and SEO optimization for static sites. This document outlines best practices for code style, structure, and performance."
category: "rules"
tags: ["Jekyll", "Ruby", "Tailwind CSS", "SEO", "Static Sites"]
tech_stack: ["jekyll", "ruby", "tailwind", "seo"]
---

You have a solid grasp of Jekyll, Ruby, Tailwind CSS, and SEO for static sites. Let’s break down how to make the most of these tools.

### Code Style and Structure
First, focus on writing Ruby code that’s both efficient and easy to maintain. Providing clear examples helps everyone understand better. When using Jekyll, aim for modular and reusable code blocks, especially for layouts, includes, and data files. Organize your content files with clear naming conventions and a logical directory structure. Descriptive variable and method names, like `siteTitle` or `generateFeed`, make it easier to understand their purpose. When structuring Jekyll templates, include layout files, reusable partials in the `_includes` folder, custom data files, and front matter.

### Naming Conventions
Next, let’s talk about naming conventions. Use lowercase letters with dashes for directory names, such as `_layouts/default.html` or `_includes/site-header.html`. Clear and descriptive names for collections, data files, and variables in `_config.yml` and front matter help keep everything organized.

### SEO and Sitemap
Now, for SEO, integrate the `jekyll-seo-tag` gem. This gem enhances your site's SEO by allowing you to configure metadata like title, description, and canonical URLs for better search indexing. You should also generate and customize a sitemap using the `jekyll-sitemap` gem. This step improves how search engines discover your site.

### Markdown and Content
When it comes to content, use the `kramdown-parser-gfm` for GitHub-flavored Markdown. This parser enables advanced Markdown features that enhance your posts. Keep your Markdown formatting and content organized consistently across all posts and pages.

### Tailwind CSS Usage
Tailwind CSS helps you implement responsive design principles effectively. Follow mobile-first design strategies to ensure your site looks great on any device. By leveraging Tailwind’s utility-first approach, you can reduce the amount of custom CSS you need.

### Performance Optimization
Performance matters a lot. Limit your use of JavaScript and external libraries to boost page load speed. Optimize images for performance by using the WebP format, including size attributes, and implementing lazy loading. Also, generate efficient RSS feeds with the `jekyll-feed` gem to keep your subscribers updated without slowing down your site.

### Linting and Code Quality
To maintain code quality, use `rubocop` to enforce Ruby best practices and keep your code clean. Ensure that your HTML structure and site code follow best practices for accessibility and performance.

### Build and Deployment
For building and deploying your site, use `jekyll-postcss` to process and optimize CSS. During local development, leverage `webrick` to preview changes efficiently.

### Key Conventions
Finally, optimize your site’s navigation and hierarchy to enhance SEO. Prioritize site speed and accessibility by minimizing the use of heavy assets. Always refer to Jekyll’s documentation for best practices regarding file structure, custom plugins, and deployment workflows. 

By following these steps, you'll create a well-structured, high-performing static site that stands out!