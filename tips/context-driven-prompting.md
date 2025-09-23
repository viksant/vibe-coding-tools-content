---
title: "Context-Driven Prompting for Better Code Generation"
description: "How to provide rich context to LLMs for more accurate code suggestions"
category: "tips-tricks"
tags: ["prompting", "context", "llm", "code-generation", "best-practices"]
tech_stack: ["any"]
---

Providing rich context when prompting LLMs can significantly enhance the accuracy of code suggestions. This approach ensures that the model understands your specific needs and the environment in which you are working. 

1. **Identify Your Tech Stack**: Clearly state the programming language, frameworks, and libraries you are using.
   - Example: `I'm using Python with Flask and SQLAlchemy.`
   
2. **Outline Project Structure**: Describe the organization of your project files and directories.
   - Example: `My project structure is: /app, /models, /routes, /templates.`
   
3. **Specify Coding Conventions**: Mention any specific coding standards or styles you follow.
   - Example: `I follow PEP 8 for Python code style.`
   
4. **Detail Specific Requirements**: Include any particular functionality or features you need help with.
   - Example: `I need a function to query the database and return user details based on user ID.`
   
5. **Combine All Context in One Prompt**: Formulate your prompt by integrating all the above elements.
   - Example: `Using Python with Flask and SQLAlchemy, in my project structure (/app, /models, /routes), following PEP 8, I need a function to query the database for user details by user ID.`

Expected result: You will receive more relevant and tailored code suggestions from the LLM.

## Why It Works
Providing detailed context helps the LLM understand your specific environment and requirements, leading to more accurate and useful code suggestions. Use this approach when you need help with complex coding tasks or when working in a unique project setup.

## Quick Examples
- **Before**: `Give me a function to get user data.`
- **After**: `Using Python with Flask and SQLAlchemy, in my project structure (/app, /models, /routes), following PEP 8, I need a function to query the database for user details by user ID.`
  
- **Before**: `How do I connect to a database?`
- **After**: `In my Node.js project using Sequelize, I need to connect to a PostgreSQL database with the following credentials: host, user, password.`

## Common Mistakes
- **Too Vague**: Avoid prompts like `Help me with a function.` 
  - **Fix**: Always include your tech stack and specific needs.
  
- **Missing Structure**: Not mentioning project organization can lead to irrelevant suggestions.
  - **Fix**: Clearly describe your project structure in the prompt.
  
- **Ignoring Conventions**: Neglecting coding standards can result in style mismatches.
  - **Fix**: State your coding conventions explicitly.
  
- **Overloading Context**: Providing excessive or irrelevant details can confuse the model.
  - **Fix**: Focus on the most pertinent information related to your request.