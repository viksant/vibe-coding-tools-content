---
title: "Use Specific Technology Versions in Prompts"
description: "Specify exact framework and library versions for accurate code generation"
category: "tips-tricks"
tags: ["prompting", "versions", "compatibility", "dependencies", "accuracy"]
tech_stack: ["any"]
---

To ensure accurate code generation, **always specify the exact versions of frameworks, libraries, and languages** in your prompts. This helps avoid compatibility issues and leverages the specific features available in those versions. 

1. **Identify the versions** of the frameworks or libraries you are using. 
   - Example: `React 17.0.2`, `Node.js 14.17.0`.
2. **Craft your prompt** to include these specific versions.
   - Example: “Generate a React component using React 17.0.2.”
3. **Use clear context** about what you want to achieve.
   - Example: “Create a form using React 17.0.2 with hooks.”
4. **Submit your prompt** to the code generation tool or AI.
   - Example: Paste your prompt into the tool.
5. **Review the generated code** to ensure it aligns with the specified versions.
   - Expected result: You receive code that utilizes the correct APIs and features for the specified versions.

### Why It Works
Specifying exact versions allows the AI to tailor its responses based on the specific APIs and features available in those versions, leading to more accurate and relevant code. Use this approach when working with libraries or frameworks that frequently update or change their APIs.

### Quick Examples
- **Before**: “Generate a React component.”
- **After**: “Generate a React component using React 17.0.2.”
  
- **Before**: “Show me how to set up an Express server.”
- **After**: “Show me how to set up an Express server using Express 4.17.1.”

### Common Mistakes
- **Not specifying versions**: Leads to outdated or incompatible code. **Fix**: Always include the version in your prompt.
- **Using vague terms**: Results in generic responses. **Fix**: Be specific about the functionality you need.
- **Ignoring breaking changes**: Can lead to errors in your code. **Fix**: Check the changelog for the versions you are using.
- **Assuming defaults**: May not reflect the latest features. **Fix**: Explicitly state the versions to ensure accuracy.