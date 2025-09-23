---
title: "Specify Exact Error Types for Better Debugging"
description: "How to get targeted debugging help by describing specific error patterns"
category: "tips-tricks"
tags: ["debugging", "error-handling", "prompting", "troubleshooting"]
tech_stack: ["any"]
---

To improve your debugging process, specify the exact error types and provide detailed context when seeking help. This approach allows others to understand the specific failure patterns and offer targeted solutions.

1. **Identify the Error Type**: Look at the error message or stack trace to determine the exact type of error (e.g., `NullReferenceException`, `SyntaxError`).
   - Example: `TypeError: Cannot read property 'foo' of undefined`
   
2. **Gather the Stack Trace**: Copy the stack trace associated with the error. This provides context about where the error occurred in your code.
   - Example: 
     ```
     at Object.<anonymous> (app.js:10:5)
     at Module._compile (module.js:652:30)
     ```

3. **Document Reproduction Steps**: Write down the exact steps to reproduce the error, including any specific inputs or actions that lead to the issue.
   - Example: 
     - Open the application
     - Click on the "Submit" button without filling out the form

4. **Prepare a Minimal Example**: If possible, create a small code snippet that reproduces the error. This helps others quickly understand the problem.
   - Example:
     ```javascript
     function submitForm(data) {
         console.log(data.foo); // Error occurs here
     }
     submitForm(undefined);
     ```

5. **Ask for Help**: When posting your question, include the error type, stack trace, reproduction steps, and minimal example.
   - Example prompt: "I'm encountering a `TypeError` when trying to access a property of `undefined`. Here’s the stack trace and reproduction steps..."

Expected result: By providing detailed information, you increase the likelihood of receiving accurate and effective debugging assistance.

### WHY IT WORKS
This method works because it gives others the necessary context to understand the issue, making it easier to diagnose and suggest solutions. Use it when you encounter persistent errors or when seeking help from forums or colleagues.

### QUICK EXAMPLES
- **Before**: "I'm getting an error."
- **After**: "I'm encountering a `TypeError: Cannot read property 'foo' of undefined`. Here’s the stack trace and steps to reproduce."
  
- **Before**: "My code doesn't work."
- **After**: "The function fails with `NullReferenceException` when called with `null`. Steps to reproduce: call `myFunction(null)`."

### COMMON MISTAKES
- **Vague Error Descriptions**: Avoid saying "I have an error." Instead, specify the error type.
- **Missing Stack Trace**: Always include the stack trace; it provides critical context.
- **Incomplete Reproduction Steps**: Ensure your steps are clear and detailed to replicate the issue accurately.
- **Not Providing a Minimal Example**: Create a concise code snippet that demonstrates the problem to facilitate understanding.