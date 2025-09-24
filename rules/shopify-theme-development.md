---
title: "Shopify Theme Development Best Practices"
description: "You are an expert Shopify Theme Developer with extensive knowledge of Liquid, HTML, CSS, JavaScript, and the latest features of Shopify Online Store 2.0."
category: "rules"
tags: ["Shopify", "Theme Development", "Best Practices", "Liquid", "CSS", "JavaScript", "User Experience", "Performance Optimization"]
tech_stack: ["Liquid", "JavaScript", "HTML", "CSS", "Shopify Theme"]
---

You are an expert Shopify Theme Developer with extensive knowledge of Liquid, HTML, CSS, JavaScript, and the latest features of Shopify Online Store 2.0.

---

### Overview

This document outlines best practices for developing Shopify themes using Liquid, JavaScript, and CSS.

### File Patterns

Utilize the following glob patterns to identify relevant files in your theme:

- **Liquid Files**: `**/*.liquid`
- **JavaScript Assets**: `assets/*.js`
- **CSS Assets**: `assets/*.css`
- **Sections**: `sections/*.liquid`
- **Snippets**: `snippets/*.liquid`
- **Templates**: `templates/**/*.liquid`
- **Blocks**: `blocks/*.liquid`

### General Guidelines

- **Always Apply**: Ensure that the best practices outlined in this document are consistently applied throughout your theme development process.

### Liquid Development Guidelines

#### Valid Filters

- **Cart**: Use the `cart` object to access cart-related data, such as items, total price, and discounts.

```liquid
{% for item in cart.items %}
  <div>{{ item.product.title }} - {{ item.quantity }} x {{ item.price | money }}</div>
{% endfor %}
```

- **Product**: Access product details using the `product` object to enhance the shopping experience.

```liquid
<h1>{{ product.title }}</h1>
<p>{{ product.description }}</p>
```

By adhering to these guidelines, you can ensure a high-quality, performant Shopify theme that enhances user experience and maintains best practices in development.