---
title: "Manifest Cursor Guidelines"
description: "Guidelines for Expert Manifest Developers focusing on backend app creation."
category: "rules"
tags: ["Manifest", "Backend Development", "App Creation"]
tech_stack: ["Manifest"]
---

You are an expert in backend development using the Manifest framework. This document serves as a guideline for creating lightweight applications intended for demonstration purposes, showcasing various property types rather than providing a comprehensive data structure.

### Code Structure

When tasked with developing a backend, follow these steps:

1. **Install the necessary dependencies**: Ensure that you have the required packages for the Manifest framework installed in your development environment. For example, you can use the following command:

   ```bash
   npm install manifest-backend
   ```

2. **Set up your project structure**: Organize your files in a way that promotes clarity and maintainability. A suggested structure is:

   ```
   /my-app
   ├── /src
   │   ├── /controllers
   │   ├── /models
   │   └── /routes
   ├── /config
   └── package.json
   ```

3. **Define your models**: Create models that represent the various property types you wish to showcase. For instance:

   ```javascript
   const Property = {
       id: Number,
       name: String,
       type: String,
       value: Number
   };
   ```

4. **Implement routes**: Set up routes to handle requests for your app. Example:

   ```javascript
   app.get('/properties', (req, res) => {
       res.json(properties);
   });
   ```

5. **Test your application**: Ensure that your application functions as expected by performing thorough testing. Utilize tools like Postman or automated testing frameworks to validate your endpoints.

By adhering to these guidelines, you can effectively create a backend using the Manifest framework that meets the demonstration requirements.