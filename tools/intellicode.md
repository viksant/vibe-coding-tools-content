---
title: "IntelliCode"
description: "Microsoft's AI-assisted development extension for Visual Studio and VS Code that enhances coding efficiency through intelligent code suggestions."
category: "tools"
tags: ["microsoft", "vscode", "visual-studio", "ai-completion", "intellisense", "team-models", "code-quality", "refactoring"]
tech_stack: ["csharp", "python", "typescript", "java", "cpp", "javascript", "ruby"]
---

### Tool Benefits
Microsoft IntelliCode makes coding smoother by using AI to offer smart IntelliSense suggestions drawn from thousands of open-source projects. Here’s what it brings to the table:

- **Contextual Suggestions**: It provides relevant code completions that fit the context of what you're writing, helping you code faster and with fewer errors.
- **Whole-Line Completions**: Instead of just suggesting snippets, IntelliCode can offer entire lines of code, cutting down on how much you need to type.
- **Custom Team Models**: Teams can create tailored models based on their own codebases. This way, suggestions match your team's unique coding style and practices.
- **Refactoring Suggestions**: It spots chances to improve your code, which helps maintain quality and makes your code easier to manage.
- **Cross-Platform Support**: IntelliCode works with both Visual Studio and VS Code, making it accessible for a variety of developers.

### Setup & Installation
#### Visual Studio
1. Launch **Visual Studio**.
2. Go to **Extensions** and select **Manage Extensions**.
3. In the **Online** section, search for **IntelliCode**.
4. Hit **Download** and follow the prompts to install.
5. Restart Visual Studio to enable the extension.

#### Visual Studio Code
1. Open **Visual Studio Code**.
2. Click on the Extensions icon in the Activity Bar to open the **Extensions** view.
3. Search for **IntelliCode**.
4. Click **Install**.
5. Reload the window when prompted.

### Configuration
- **Enable/Disable IntelliCode**: Head to `File`, then `Preferences`, and click on `Settings`. Search for `IntelliCode` and toggle the settings as needed.
- **Custom Team Models**: To use team models, make sure you have access to the Azure DevOps organization where the models reside. Use the command palette (`Ctrl+Shift+P`) and enter `IntelliCode: Get Team Models`.
- **Adjust Completion Behavior**: Tweak settings like `Editor: Quick Suggestions` to manage when suggestions pop up.

### Usage Guide
- **Basic Usage**: As you start typing a method or variable name, IntelliCode will offer completions. Use the arrow keys to scroll through suggestions and hit `Tab` to accept one.
- **Whole-Line Completion**: Begin typing a line, and IntelliCode will suggest a complete line of code. For instance, typing `for` will bring up a full for-loop structure.
- **Refactoring**: Highlight a section of code, right-click, and choose **Refactor** to see suggestions for improving your code.

### Advanced Features
- **Custom Models**: You can train IntelliCode on your own codebase with the command `IntelliCode: Train Model`, but you'll need a connection to Azure DevOps.
- **Integration with GitHub**: IntelliCode can analyze your GitHub repositories to give you suggestions tailored to your coding habits.
- **Multi-Language Support**: It works well with various languages, including C#, Python, TypeScript, and more. Make sure to use the right language extensions for better support.

### Troubleshooting
- **IntelliCode Not Suggesting**: First, check if IntelliCode is enabled in your settings. Also, look for conflicts with other extensions.
- **Slow Performance**: If IntelliCode runs slowly, try disabling other extensions temporarily to see if there are conflicts. Also, ensure your system meets the minimum requirements.
- **Model Training Issues**: If problems arise while training custom models, check your Azure DevOps permissions and confirm that the repository is accessible.

### Best Practices
- **Use Team Models**: Take advantage of custom team models to ensure suggestions align with your team's coding standards.
- **Regularly Update**: Keep IntelliCode updated to enjoy the latest features and enhancements.
- **Combine with Other Tools**: Pair IntelliCode with other code quality tools like linters and formatters for the best results.
- **Explore Settings**: Regularly review and adjust settings based on your workflow to boost your productivity.