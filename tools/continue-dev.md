---
title: "Continue.dev"
description: "Open-source AI code assistant for VS Code and JetBrains IDEs, providing intelligent code completion, explanation, and refactoring suggestions."
category: "tools"
tags: ["ai-assistant", "vscode-extension", "jetbrains", "open-source", "code-completion", "chat", "code-refactoring", "llm-integration"]
tech_stack: ["JavaScript", "TypeScript", "Python", "Java", "C#", "Node.js", "VS Code", "JetBrains IDEs"]
---

### Tool Benefits
Continue.dev is an open-source AI coding assistant that fits right into your IDE, bringing several handy features:
- **Intelligent Code Completion**: It gives you context-aware suggestions that help you code faster.
- **Code Explanation**: Automatically explains snippets of code, making it easier to grasp complex logic.
- **Refactoring Suggestions**: It recommends ways to improve your code's structure and readability.
- **Multi-Provider Support**: Works with various LLM providers like GPT-4, Claude, and local models, giving you flexibility and privacy.
- **Enhanced Productivity**: It cuts down the time spent on coding tasks, letting you focus on higher-level design and problem-solving.

### Setup & Installation
#### For Visual Studio Code
1. Open VS Code.
2. Click on the Extensions icon in the Activity Bar on the side.
3. Type `Continue.dev` in the Extensions Marketplace search bar.
4. Hit the **Install** button.

#### For JetBrains IDEs
1. Open your JetBrains IDE (like IntelliJ IDEA or PyCharm).
2. Go to `File` > `Settings` (or `Preferences` on macOS).
3. Select `Plugins` from the left sidebar.
4. Search for `Continue.dev` in the Marketplace tab.
5. Click the **Install** button and restart the IDE.

### Configuration
Once you've installed Continue.dev, it's time to configure it for your needs:
1. Open the settings for Continue.dev in your IDE.
2. Choose your preferred LLM provider:
   - For GPT-4: `{"provider": "gpt-4"}`
   - For Claude: `{"provider": "claude"}`
   - For local models: `{"provider": "local", "model_path": "/path/to/model"}`
3. Tweak the completion settings:
   - **Max Tokens**: Set the maximum number of tokens for suggestions, e.g., `{"max_tokens": 100}`.
   - **Temperature**: Adjust the randomness of responses, e.g., `{"temperature": 0.7}`.

### Usage Guide
Here’s how to get the most out of Continue.dev:
- **Code Completion**: Start typing a function name or variable, and suggestions will pop up. Press `Tab` to accept one.
- **Code Explanation**: Highlight a code block and call Continue.dev (often via a shortcut like `Ctrl+Shift+E`) to get an explanation.
- **Refactoring**: Select a piece of code and use the refactor command (like `Ctrl+Shift+R`) to receive suggestions for improvements.

Check this example for code explanation:
```javascript
// Highlight this code and invoke explanation
function calculateSum(a, b) {
    return a + b;
}
```

### Advanced Features
Dig deeper with these advanced features:
- **Custom Shortcuts**: Set up your own keyboard shortcuts for quick access to features.
- **Integration with Git**: Analyze code changes and get suggestions based on diffs with Continue.dev.
- **Local Model Support**: Run models locally for better privacy and performance, especially with sensitive projects.

### Troubleshooting
If you run into issues:
- **Installation Problems**: Make sure your IDE is updated to the latest version and that it’s compatible with your operating system.
- **No Suggestions**: Check that the LLM provider is set up correctly in the settings.
- **Slow Performance**: If you’re using a local model, ensure your machine meets the necessary hardware requirements.

### Best Practices
Keep these tips in mind:
- Regularly update Continue.dev to enjoy the latest features and improvements.
- Try out different LLM providers to see which one fits your workflow best.
- Use code explanations to deepen your understanding of unfamiliar codebases.
- Make Continue.dev a part of your daily coding routine to boost productivity and improve code quality.