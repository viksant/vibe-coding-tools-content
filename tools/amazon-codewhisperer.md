---
title: "Amazon CodeWhisperer"
description: "AI coding companion that provides real-time code suggestions and security scanning to enhance developer productivity and code quality."
category: "tools"
tags: ["ai-assistant", "aws", "code-suggestions", "security-scanning", "autocomplete", "amazon"]
tech_stack: ["python", "java", "javascript", "typescript", "c#", "go", "rust", "php", "ruby", "kotlin", "c", "c++", "shell", "sql"]
---

### Tool Benefits
Amazon CodeWhisperer is an AI-powered coding assistant that enhances developer productivity by providing real-time code suggestions based on comments and existing code. Key benefits include:
- **Real-time Code Suggestions**: Generates context-aware code snippets as you type, reducing the time spent on writing boilerplate code.
- **Security Scanning**: Automatically scans for security vulnerabilities and suggests fixes, helping maintain secure code practices.
- **Multi-language Support**: Supports over 15 programming languages, making it versatile for various development projects.
- **IDE Integration**: Seamlessly integrates with popular IDEs like VS Code, IntelliJ, and AWS Cloud9, fitting into existing workflows.

### Setup & Installation
To install Amazon CodeWhisperer, follow these steps based on your IDE:

#### Visual Studio Code
1. Open VS Code.
2. Go to the Extensions view by clicking on the Extensions icon in the Activity Bar on the side of the window.
3. Search for "Amazon CodeWhisperer".
4. Click **Install** on the Amazon CodeWhisperer extension.
5. After installation, reload VS Code.

#### IntelliJ IDEA
1. Open IntelliJ IDEA.
2. Navigate to `File` > `Settings` (or `IntelliJ IDEA` > `Preferences` on macOS).
3. Select `Plugins` from the left sidebar.
4. Search for "Amazon CodeWhisperer" in the Marketplace.
5. Click **Install** and restart IntelliJ IDEA.

#### AWS Cloud9
1. Open your AWS Cloud9 environment.
2. Navigate to the `AWS Cloud9` menu.
3. Select `Preferences`.
4. Under `AWS`, find the `CodeWhisperer` section and enable it.

### Configuration
After installation, configure Amazon CodeWhisperer to suit your development needs:

- **Enable Code Suggestions**: 
  - In VS Code, go to `Settings` and search for "CodeWhisperer". Ensure the option for code suggestions is enabled.
- **Set Language Preferences**: 
  - Specify preferred programming languages in the settings to optimize suggestions.
- **Security Scanning Settings**: 
  - Enable or disable security scanning based on project requirements in the settings menu.

### Usage Guide
Here are practical examples of how to use Amazon CodeWhisperer effectively:

#### Example 1: Generating a Function
```python
# Function to calculate factorial
def factorial(n):
    # CodeWhisperer will suggest the implementation here
```
As you type the comment, CodeWhisperer will provide a suggestion for the factorial function.

#### Example 2: Security Vulnerability Detection
```javascript
// Example of a potential SQL injection
const query = "SELECT * FROM users WHERE id = " + userId;
```
CodeWhisperer will highlight this line and suggest using parameterized queries instead.

### Advanced Features
- **Custom Code Templates**: Create and save custom code snippets for frequently used patterns.
- **Integration with AWS Services**: Leverage AWS SDKs and services directly within your code suggestions.
- **Collaboration Features**: Use CodeWhisperer in team settings to maintain consistent coding standards and practices.

### Troubleshooting
- **Code Suggestions Not Appearing**: Ensure that the extension is enabled and that you have the correct language mode active in your IDE.
- **Slow Performance**: Check your internet connection, as CodeWhisperer relies on cloud-based AI models. Consider adjusting your IDE settings to optimize performance.
- **Security Scanning Not Working**: Verify that security scanning is enabled in the settings and that your code adheres to the expected formats.

### Best Practices
- **Use Descriptive Comments**: Write clear comments before code blocks to guide CodeWhisperer in generating relevant suggestions.
- **Review Suggestions**: Always review the suggestions provided by CodeWhisperer, especially for security-related code.
- **Regularly Update the Extension**: Keep your CodeWhisperer extension updated to benefit from the latest features and improvements.
- **Combine with Code Reviews**: Use CodeWhisperer alongside peer code reviews to enhance code quality and security.

This guide provides a comprehensive overview of Amazon CodeWhisperer, enabling developers to set up, configure, and use the tool effectively in their development workflows.