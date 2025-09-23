---
title: "Continue.dev"
description: "Open-source AI code assistant for VS Code and JetBrains IDEs, providing intelligent code completion, explanation, and refactoring suggestions."
category: "tools"
tags: ["ai-assistant", "vscode-extension", "jetbrains", "open-source", "code-completion", "chat", "code-refactoring", "llm-integration"]
tech_stack: ["JavaScript", "TypeScript", "Python", "Java", "C#", "Node.js", "VS Code", "JetBrains IDEs"]
---

### Tool Benefits
Continue.dev is an open-source AI coding assistant that integrates seamlessly into your IDE, offering several advantages:
- **Intelligent Code Completion**: Provides context-aware suggestions to speed up coding.
- **Code Explanation**: Automatically explains code snippets, making it easier to understand complex logic.
- **Refactoring Suggestions**: Offers recommendations for improving code structure and readability.
- **Multi-Provider Support**: Works with various LLM providers like GPT-4, Claude, and local models, allowing for flexibility and privacy.
- **Enhanced Productivity**: Reduces the time spent on coding tasks, enabling developers to focus on higher-level design and problem-solving.

### Setup & Installation
#### For Visual Studio Code
1. Open VS Code.
2. Go to the Extensions view by clicking on the Extensions icon in the Activity Bar on the side.
3. Search for `Continue.dev` in the Extensions Marketplace.
4. Click on the **Install** button.

#### For JetBrains IDEs
1. Open your JetBrains IDE (e.g., IntelliJ IDEA, PyCharm).
2. Navigate to `File` > `Settings` (or `Preferences` on macOS).
3. Select `Plugins` from the left sidebar.
4. Search for `Continue.dev` in the Marketplace tab.
5. Click on the **Install** button and restart the IDE.

### Configuration
After installation, configure Continue.dev to suit your development needs:
1. Open the settings for Continue.dev in your IDE.
2. Set your preferred LLM provider:
   - For GPT-4: `{"provider": "gpt-4"}`
   - For Claude: `{"provider": "claude"}`
   - For local models: `{"provider": "local", "model_path": "/path/to/model"}`
3. Adjust the completion settings:
   - **Max Tokens**: Set the maximum number of tokens for suggestions, e.g., `{"max_tokens": 100}`.
   - **Temperature**: Control the randomness of responses, e.g., `{"temperature": 0.7}`.

### Usage Guide
To effectively use Continue.dev:
- **Code Completion**: Start typing a function name or variable, and suggestions will appear. Use `Tab` to accept a suggestion.
- **Code Explanation**: Highlight a code block and invoke Continue.dev (usually via a shortcut like `Ctrl+Shift+E`) to get an explanation.
- **Refactoring**: Select a piece of code and use the refactor command (e.g., `Ctrl+Shift+R`) to get suggestions for improvements.

Example command for code explanation:
```javascript
// Highlight this code and invoke explanation
function calculateSum(a, b) {
    return a + b;
}
```

### Advanced Features
- **Custom Shortcuts**: Configure custom keyboard shortcuts for quick access to features.
- **Integration with Git**: Use Continue.dev to analyze code changes and suggest improvements based on diffs.
- **Local Model Support**: Run models locally for enhanced privacy and performance, especially in sensitive projects.

### Troubleshooting
- **Installation Issues**: Ensure your IDE is updated to the latest version. Check for compatibility with your operating system.
- **No Suggestions Appearing**: Verify that the LLM provider is correctly configured in the settings.
- **Slow Performance**: If using a local model, ensure your machine meets the necessary hardware requirements.

### Best Practices
- Regularly update Continue.dev to benefit from the latest features and improvements.
- Experiment with different LLM providers to find the one that best fits your workflow.
- Use code explanations to deepen your understanding of unfamiliar codebases.
- Incorporate Continue.dev into your daily coding routine to maximize productivity and code quality.