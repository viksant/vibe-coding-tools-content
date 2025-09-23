---
title: "IntelliCode"
description: "Microsoft's AI-assisted development extension for Visual Studio and VS Code that enhances coding efficiency through intelligent code suggestions."
category: "tools"
tags: ["microsoft", "vscode", "visual-studio", "ai-completion", "intellisense", "team-models", "code-quality", "refactoring"]
tech_stack: ["csharp", "python", "typescript", "java", "cpp", "javascript", "ruby"]
---

### Tool Benefits
**Microsoft IntelliCode** enhances the development experience by providing AI-driven IntelliSense suggestions based on best practices from thousands of open-source projects. Key benefits include:
- **Contextual Suggestions**: Offers relevant code completions based on the context of your code, improving coding speed and accuracy.
- **Whole-Line Completions**: Suggests entire lines of code, reducing the amount of typing required.
- **Custom Team Models**: Allows teams to create models based on their own codebases, ensuring suggestions align with team-specific coding styles and practices.
- **Refactoring Suggestions**: Identifies opportunities for code improvements, enhancing code quality and maintainability.
- **Cross-Platform Support**: Available for both Visual Studio and VS Code, catering to a wide range of developers.

### Setup & Installation
#### Visual Studio
1. Open **Visual Studio**.
2. Navigate to **Extensions** > **Manage Extensions**.
3. Search for **IntelliCode** in the **Online** section.
4. Click **Download** and follow the prompts to install.
5. Restart Visual Studio to activate the extension.

#### Visual Studio Code
1. Open **Visual Studio Code**.
2. Go to the **Extensions** view by clicking on the Extensions icon in the Activity Bar.
3. Search for **IntelliCode**.
4. Click **Install**.
5. Reload the window when prompted.

### Configuration
- **Enable/Disable IntelliCode**: Go to `File` > `Preferences` > `Settings`, search for `IntelliCode`, and toggle the settings as needed.
- **Custom Team Models**: To use team models, ensure you have access to the Azure DevOps organization where the models are hosted. Use the command palette (`Ctrl+Shift+P`) and type `IntelliCode: Get Team Models`.
- **Adjust Completion Behavior**: Modify settings such as `Editor: Quick Suggestions` to control when suggestions appear.

### Usage Guide
- **Basic Usage**: Start typing a method or variable name, and IntelliCode will suggest completions. Use the arrow keys to navigate suggestions and `Tab` to accept.
- **Whole-Line Completion**: Type the beginning of a line, and IntelliCode will suggest a full line of code. For example, typing `for` will suggest a complete for-loop structure.
- **Refactoring**: Highlight a piece of code, right-click, and select **Refactor** to see suggestions for improving your code.

### Advanced Features
- **Custom Models**: Train IntelliCode on your codebase by using the command `IntelliCode: Train Model`. This requires a connection to Azure DevOps.
- **Integration with GitHub**: IntelliCode can analyze your GitHub repositories to provide tailored suggestions based on your coding patterns.
- **Multi-Language Support**: Works seamlessly across multiple languages, including C#, Python, TypeScript, and more. Use the appropriate language extensions for enhanced support.

### Troubleshooting
- **IntelliCode Not Suggesting**: Ensure that IntelliCode is enabled in your settings. Check for any conflicts with other extensions.
- **Slow Performance**: If IntelliCode is slow, consider disabling other extensions temporarily to identify conflicts. Also, ensure your system meets the minimum requirements.
- **Model Training Issues**: If you encounter issues while training custom models, verify your Azure DevOps permissions and ensure the repository is accessible.

### Best Practices
- **Use Team Models**: Leverage custom team models to ensure suggestions are aligned with your team's coding standards.
- **Regularly Update**: Keep IntelliCode updated to benefit from the latest features and improvements.
- **Combine with Other Tools**: Use IntelliCode alongside other code quality tools like linters and formatters for optimal results.
- **Explore Settings**: Regularly review and adjust settings based on your workflow to maximize productivity.