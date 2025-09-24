---
title: "Use Specific Technology Versions in Prompts"
description: "Specify exact framework and library versions for accurate code generation"
category: "tips-tricks"
tags: ["prompting", "versions", "compatibility", "dependencies", "accuracy"]
tech_stack: ["any"]
---

To generate code accurately, always mention the specific versions of frameworks, libraries, and languages in your prompts. This practice helps you avoid compatibility issues and makes sure you can take advantage of the unique features those versions offer.

1. Start by identifying the versions of the frameworks or libraries you are using.  
   - For instance, you might use `React 17.0.2` or `Node.js 14.17.0`.
  
2. Next, craft your prompt to include these specific versions.  
   - For example, say, “Generate a React component using React 17.0.2.”

3. Provide clear context about what you want to achieve.  
   - You could say, “Create a form using React 17.0.2 with hooks.”

4. Submit your prompt to the code generation tool or AI.  
   - Just paste your prompt into the tool.

5. Finally, review the generated code to ensure it matches the specified versions.  
   - You should get code that uses the correct APIs and features for the versions you mentioned.

### Why This Matters
When you specify exact versions, the AI can customize its responses based on the specific APIs and features available in those versions. This approach leads to more accurate and applicable code, especially when working with libraries or frameworks that often update.

### Quick Examples
- **Before**: “Generate a React component.”  
- **After**: “Generate a React component using React 17.0.2.”

- **Before**: “Show me how to set up an Express server.”  
- **After**: “Show me how to set up an Express server using Express 4.17.1.”

### Common Mistakes
- **Not specifying versions**: This can lead to outdated or incompatible code. **Fix**: Always include the version in your prompt.
  
- **Using vague terms**: This often results in generic responses. **Fix**: Be specific about the functionality you need.

- **Ignoring breaking changes**: This may cause errors in your code. **Fix**: Check the changelog for the versions you are using.

- **Assuming defaults**: This might not reflect the latest features. **Fix**: Clearly state the versions to ensure accuracy.