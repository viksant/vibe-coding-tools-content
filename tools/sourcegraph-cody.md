---
title: "Sourcegraph Cody"
description: "AI coding assistant with codebase context understanding, providing intelligent code completion, explanations, and answers based on your specific repository."
category: "tools"
tags: ["ai-assistant", "codebase-context", "enterprise", "vscode", "jetbrains", "chat", "code-completion", "team-collaboration"]
tech_stack: ["JavaScript", "TypeScript", "Python", "Java", "Go", "C#", "Ruby", "PHP"]
---

### Tool Benefits
**Sourcegraph Cody** is an AI coding assistant that enhances developer productivity by providing context-aware code suggestions and explanations. Key benefits include:
- **Context Understanding**: Leverages the entire codebase context to offer relevant code completions and insights.
- **Intelligent Code Completion**: Reduces coding time by suggesting code snippets based on the current context and previous code.
- **Explanations and Answers**: Provides explanations for code snippets and answers to queries related to the codebase.
- **Collaboration Features**: Facilitates team collaboration by sharing insights and suggestions among team members.
- **Free and Enterprise Versions**: Offers a scalable solution for both individual developers and large teams with advanced features.

### Setup & Installation
#### For Visual Studio Code
1. Open **Visual Studio Code**.
2. Go to the Extensions view by clicking on the Extensions icon in the Activity Bar on the side or pressing `Ctrl+Shift+X`.
3. Search for "Sourcegraph Cody" in the Extensions Marketplace.
4. Click **Install** to add the extension.
5. After installation, reload Visual Studio Code.

#### For JetBrains IDEs
1. Open your JetBrains IDE (e.g., IntelliJ IDEA, PyCharm).
2. Navigate to **File > Settings > Plugins**.
3. Click on the Marketplace tab and search for "Sourcegraph Cody".
4. Click **Install** and restart the IDE.

#### For Command Line Installation
1. Ensure you have Node.js installed. Check by running:
   ```bash
   node -v
   ```
2. Install the Sourcegraph CLI globally:
   ```bash
   npm install -g sourcegraph-cli
   ```
3. Authenticate with your Sourcegraph instance:
   ```bash
   sourcegraph login <your-instance-url>
   ```

### Configuration
1. Open the settings for Sourcegraph Cody in your IDE.
2. Configure the following options:
   - **API URL**: Set the URL of your Sourcegraph instance.
   - **Enable/Disable Features**: Toggle features like code completion, explanations, and chat.
   - **Team Collaboration**: Set permissions for team members to access shared insights.
3. Save and apply the settings.

### Usage Guide
- **Code Completion**: Start typing a function or variable name, and Cody will suggest completions based on the context.
- **Code Explanations**: Highlight a code snippet and invoke Cody to get an explanation:
  ```plaintext
  Highlight code -> Right-click -> Ask Cody
  ```
- **Chat with Cody**: Use the integrated chat feature to ask questions about the codebase:
  ```plaintext
  Type your question in the chat window and hit Enter.
  ```

### Advanced Features
- **Integrations**: Connect Cody with other tools like Slack or Jira for enhanced collaboration.
- **Custom Commands**: Create custom commands for frequently used snippets or queries.
- **Performance Optimization**: Regularly index your codebase to improve response times and accuracy of suggestions.

### Troubleshooting
- **Cody Not Responding**: Ensure your Sourcegraph instance is running and accessible. Check your API URL in the settings.
- **Slow Performance**: Optimize your codebase indexing settings and ensure your IDE has sufficient resources allocated.
- **Installation Issues**: Verify that your IDE version is compatible with the Sourcegraph Cody extension.

### Best Practices
- Regularly update the Sourcegraph Cody extension to benefit from the latest features and improvements.
- Utilize the chat feature to clarify complex code segments and share insights with team members.
- Encourage team collaboration by sharing code snippets and explanations through the integrated features.
- Customize Cody's settings based on your workflow preferences for optimal performance.