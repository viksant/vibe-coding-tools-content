---
title: "Context-Driven Prompting for Better Code Generation"
description: "How to provide rich context to LLMs for more accurate code suggestions"
category: "tips-tricks"
tags: ["prompting", "context", "llm", "code-generation", "best-practices"]
tech_stack: ["any"]
---

Providing clear context when you prompt LLMs can really boost the accuracy of the code they suggest. By doing this, you help the model grasp your specific needs and the environment you’re working in.

### 1. Identify Your Tech Stack
Start by clearly stating the programming language, frameworks, and libraries you’re using.  
*Example*: “I’m using Python with Flask and SQLAlchemy.”

### 2. Outline Project Structure
Next, describe how your project files and directories are organized.  
*Example*: “My project structure is: /app, /models, /routes, /templates.”

### 3. Specify Coding Conventions
Mention any specific coding standards or styles you follow.  
*Example*: “I follow PEP 8 for Python code style.”

### 4. Detail Specific Requirements
Include any specific functionality or features you need help with.  
*Example*: “I need a function to query the database and return user details based on user ID.”

### 5. Combine All Context in One Prompt
Finally, put everything together to form a comprehensive prompt.  
*Example*: “Using Python with Flask and SQLAlchemy, in my project structure (/app, /models, /routes), following PEP 8, I need a function to query the database for user details by user ID.”

### Expected Result
This approach will lead to more relevant and tailored code suggestions from the LLM.

## Why It Works
Providing detailed context helps the LLM understand your unique environment and requirements. This detail results in more accurate and useful code suggestions. Use this method when tackling complex coding tasks or when you’re working on a distinctive project setup.

## Quick Examples
- **Before**: “Give me a function to get user data.”  
- **After**: “Using Python with Flask and SQLAlchemy, in my project structure (/app, /models, /routes), following PEP 8, I need a function to query the database for user details by user ID.”

- **Before**: “How do I connect to a database?”  
- **After**: “In my Node.js project using Sequelize, I need to connect to a PostgreSQL database with the following credentials: host, user, password.”

## Common Mistakes
- **Too Vague**: Avoid prompts like “Help me with a function.”  
  **Fix**: Always include your tech stack and specific needs.

- **Missing Structure**: Not mentioning project organization can lead to irrelevant suggestions.  
  **Fix**: Clearly describe your project structure in the prompt.

- **Ignoring Conventions**: Neglecting coding standards can result in style mismatches.  
  **Fix**: State your coding conventions explicitly.

- **Overloading Context**: Providing too many irrelevant details can confuse the model.  
  **Fix**: Focus on the most important information related to your request.