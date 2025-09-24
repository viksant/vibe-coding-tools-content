---
title: "Amazon CodeWhisperer"
description: "AI coding companion that provides real-time code suggestions and security scanning to enhance developer productivity and code quality."
category: "tools"
tags: ["ai-assistant", "aws", "code-suggestions", "security-scanning", "autocomplete", "amazon"]
tech_stack: ["python", "java", "javascript", "typescript", "c#", "go", "rust", "php", "ruby", "kotlin", "c", "c++", "shell", "sql"]
---

### Tool Benefits
Amazon CodeWhisperer acts as a coding assistant that boosts developer productivity by offering real-time code suggestions based on your comments and existing code. Here’s what makes it stand out:

- **Real-time Code Suggestions**: It generates code snippets that fit the context as you type, helping you write less boilerplate code.
- **Security Scanning**: The tool automatically checks for security vulnerabilities and suggests fixes, which helps you keep your code safe.
- **Multi-language Support**: With support for over 15 programming languages, it fits well into various development projects.
- **IDE Integration**: It works smoothly with popular IDEs like VS Code, IntelliJ, and AWS Cloud9, making it easy to incorporate into your current workflow.

### Setup & Installation
Getting started with Amazon CodeWhisperer is simple. Here’s how to install it based on your IDE:

#### Visual Studio Code
1. Open VS Code.
2. Click on the Extensions icon in the Activity Bar on the side.
3. Type "Amazon CodeWhisperer" in the search bar.
4. Click **Install** on the Amazon CodeWhisperer extension.
5. Once it's installed, reload VS Code.

#### IntelliJ IDEA
1. Open IntelliJ IDEA.
2. Go to `File` > `Settings` (or `IntelliJ IDEA` > `Preferences` on macOS).
3. Click on `Plugins` in the left sidebar.
4. Search for "Amazon CodeWhisperer" in the Marketplace.
5. Hit **Install** and restart IntelliJ IDEA.

#### AWS Cloud9
1. Open your AWS Cloud9 environment.
2. Click on the `AWS Cloud9` menu.
3. Select `Preferences`.
4. In the `AWS` section, find `CodeWhisperer` and enable it.

### Configuration
Once you have installed Amazon CodeWhisperer, you can configure it to fit your needs:

- **Enable Code Suggestions**: 
  - In VS Code, navigate to `Settings`, search for "CodeWhisperer", and ensure code suggestions are turned on.
- **Set Language Preferences**: 
  - Specify your preferred programming languages in the settings to enhance the relevance of suggestions.
- **Security Scanning Settings**: 
  - Choose whether to enable or disable security scanning based on your project requirements in the settings menu.

### Usage Guide
Here are some practical examples of how to make the most of Amazon CodeWhisperer:

#### Example 1: Generating a Function
```python
# Function to calculate factorial
def factorial(n):
    # CodeWhisperer will suggest the implementation here
```
As you type that comment, CodeWhisperer will offer a suggestion for how to implement the factorial function.

#### Example 2: Security Vulnerability Detection
```javascript
// Example of a potential SQL injection
const query = "SELECT * FROM users WHERE id = " + userId;
```
CodeWhisperer will highlight this line and recommend using parameterized queries instead.

### Advanced Features
- **Custom Code Templates**: You can create and save snippets for patterns you use often.
- **Integration with AWS Services**: Access AWS SDKs and services directly in your code suggestions.
- **Collaboration Features**: Work with CodeWhisperer in team settings to maintain consistent coding practices.

### Troubleshooting
If you run into issues, here are some quick fixes:

- **Code Suggestions Not Appearing**: Make sure the extension is enabled and that the correct language mode is active in your IDE.
- **Slow Performance**: Check your internet connection since CodeWhisperer depends on cloud-based AI models. You might also adjust your IDE settings to improve performance.
- **Security Scanning Not Working**: Confirm that security scanning is enabled in the settings and that your code follows the expected formats.

### Best Practices
To get the most out of Amazon CodeWhisperer, consider these tips:

- **Use Descriptive Comments**: Clear comments before code blocks help guide CodeWhisperer in generating useful suggestions.
- **Review Suggestions**: Always check the suggestions from CodeWhisperer, especially when it comes to security-related code.
- **Regularly Update the Extension**: Keep your CodeWhisperer extension current to take advantage of new features and enhancements.
- **Combine with Code Reviews**: Using CodeWhisperer alongside peer code reviews can improve code quality and security.

This guide gives you a solid understanding of Amazon CodeWhisperer, helping developers set up, configure, and effectively use the tool in their workflows.