---
title: "Manifest Cursor Guidelines"
description: "Guidelines for Expert Manifest Developers focusing on backend app creation."
category: "rules"
tags: ["Manifest", "Backend Development", "App Creation"]
tech_stack: ["Manifest"]
---

You have a solid understanding of backend development with the Manifest framework. This guide will help you create lightweight applications designed for demo purposes, showcasing different property types without going into extensive data structure details.

### Code Structure

Let’s break down the steps for developing your backend:

1. **Install the necessary dependencies**: Start by installing the required packages for the Manifest framework in your development setup. You can do this using the following command:

   ```bash
   npm install manifest-backend
   ```

2. **Set up your project structure**: Organize your files to keep everything clear and easy to maintain. Here’s a suggested structure:

   ```
   /my-app
   ├── /src
   │   ├── /controllers
   │   ├── /models
   │   └── /routes
   ├── /config
   └── package.json
   ```

3. **Define your models**: Create models that represent the property types you want to display. For example:

   ```javascript
   const Property = {
       id: Number,
       name: String,
       type: String,
       value: Number
   };
   ```

4. **Implement routes**: Set up routes to manage requests for your app. Here’s a simple example:

   ```javascript
   app.get('/properties', (req, res) => {
       res.json(properties);
   });
   ```

5. **Test your application**: Make sure your application works as intended by running thorough tests. You can use tools like Postman or automated testing frameworks to check your endpoints.

Following these steps will help you successfully create a backend using the Manifest framework that fulfills your demonstration needs.