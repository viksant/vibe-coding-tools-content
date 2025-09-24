---
title: "Specify Exact Error Types for Better Debugging"
description: "How to get targeted debugging help by describing specific error patterns"
category: "tips-tricks"
tags: ["debugging", "error-handling", "prompting", "troubleshooting"]
tech_stack: ["any"]
---

To make your debugging process smoother, it's important to be specific about the errors you're encountering. This helps others provide you with the best possible solutions. Let’s break down how to do this effectively.

1. **Identify the Error Type**: Start by examining the error message or stack trace to pinpoint the exact error type, such as `NullReferenceException` or `SyntaxError`.
   - For example: `TypeError: Cannot read property 'foo' of undefined`
   
2. **Gather the Stack Trace**: Make sure to copy the stack trace related to the error. This gives important context about where the issue is occurring in your code.
   - Example:
     ```
     at Object.<anonymous> (app.js:10:5)
     at Module._compile (module.js:652:30)
     ```

3. **Document Reproduction Steps**: Clearly outline the steps needed to reproduce the error. Include any specific inputs or actions that lead to the issue.
   - For instance: 
     - Open the application
     - Click on the "Submit" button without filling in the form

4. **Prepare a Minimal Example**: If you can, create a small code snippet that reproduces the error. This allows others to grasp the problem quickly.
   - Example:
     ```javascript
     function submitForm(data) {
         console.log(data.foo); // Error occurs here
     }
     submitForm(undefined);
     ```

5. **Ask for Help**: When you ask for assistance, share the error type, stack trace, reproduction steps, and your minimal example.
   - For example, you might say: "I'm encountering a `TypeError` when trying to access a property of `undefined`. Here’s the stack trace and my reproduction steps..."

By providing detailed information, you boost your chances of getting precise and helpful debugging support.

### Why This Works
This approach is effective because it gives others the context they need to understand your issue. With that clarity, they can diagnose the problem more easily and offer relevant solutions. Use these techniques when you run into stubborn errors or when you need assistance from forums or colleagues.

### Quick Examples
- **Before**: "I'm getting an error."
- **After**: "I'm encountering a `TypeError: Cannot read property 'foo' of undefined`. Here’s the stack trace and steps to reproduce."
  
- **Before**: "My code doesn't work."
- **After**: "The function fails with `NullReferenceException` when called with `null`. Steps to reproduce: call `myFunction(null)`."

### Common Mistakes
- **Vague Error Descriptions**: Avoid general statements like "I have an error." Be specific about the error type.
- **Missing Stack Trace**: Always include the stack trace; it offers vital context.
- **Incomplete Reproduction Steps**: Make sure your steps are clear and detailed so others can replicate the issue accurately.
- **Not Providing a Minimal Example**: Share a concise code snippet to help others understand the problem quickly.