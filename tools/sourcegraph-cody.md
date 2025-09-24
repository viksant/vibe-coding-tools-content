---
title: "Sourcegraph Cody"
description: "AI coding assistant with codebase context understanding, providing intelligent code completion, explanations, and answers based on your specific repository."
category: "tools"
tags: ["ai-assistant", "codebase-context", "enterprise", "vscode", "jetbrains", "chat", "code-completion", "team-collaboration"]
tech_stack: ["JavaScript", "TypeScript", "Python", "Java", "Go", "C#", "Ruby", "PHP"]
---

### Tool Benefits

**Sourcegraph Cody** serves as an AI coding assistant designed to boost developer productivity with helpful code suggestions and explanations. Here’s what makes it stand out:

- **Context Understanding**: Cody analyzes the entire codebase to provide relevant code completions and insights tailored to your current work.
- **Intelligent Code Completion**: It saves you time by suggesting code snippets that fit your current context and past coding patterns.
- **Explanations and Answers**: Cody explains code snippets and answers questions related to your codebase, making it easier to understand your work.
- **Collaboration Features**: Team collaboration gets easier with the ability to share insights and suggestions among team members.
- **Free and Enterprise Versions**: There’s a version for everyone, whether you're an individual developer or part of a larger team needing advanced features.

### Setup & Installation

#### For Visual Studio Code
1. Launch **Visual Studio Code**.
2. Access the Extensions view by clicking the Extensions icon in the Activity Bar on the side or pressing `Ctrl+Shift+X`.
3. Search for "Sourcegraph Cody" in the Extensions Marketplace.
4. Click **Install** to add the extension.
5. Once installed, reload Visual Studio Code.

#### For JetBrains IDEs
1. Open your JetBrains IDE, like IntelliJ IDEA or PyCharm.
2. Go to **File > Settings > Plugins**.
3. Click on the Marketplace tab and search for "Sourcegraph Cody".
4. Hit **Install** and restart the IDE.

#### For Command Line Installation
1. Make sure you have Node.js installed. Check by running:
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
2. Adjust the following options:
   - **API URL**: Enter the URL of your Sourcegraph instance.
   - **Enable/Disable Features**: Toggle features like code completion, explanations, and chat.
   - **Team Collaboration**: Set permissions for team members to access shared insights.
3. Save and apply your settings.

### Usage Guide

- **Code Completion**: Just start typing a function or variable name, and Cody will suggest completions based on your context.
- **Code Explanations**: Highlight a code snippet and ask Cody for an explanation:
  ```plaintext
  Highlight code -> Right-click -> Ask Cody
  ```
- **Chat with Cody**: Use the integrated chat feature to ask questions about the codebase:
  ```plaintext
  Type your question in the chat window and hit Enter.
  ```

### Advanced Features

- **Integrations**: Connect Cody with tools like Slack or Jira to enhance collaboration.
- **Custom Commands**: Set up custom commands for frequently used snippets or queries.
- **Performance Optimization**: Regularly index your codebase to boost response times and the accuracy of suggestions.

### Troubleshooting

- **Cody Not Responding**: Make sure your Sourcegraph instance is up and running. Double-check your API URL in the settings.
- **Slow Performance**: Optimize your codebase indexing settings and ensure your IDE has enough resources allocated.
- **Installation Issues**: Confirm that your IDE version is compatible with the Sourcegraph Cody extension.

### Best Practices

- Keep the Sourcegraph Cody extension updated to take advantage of the latest features and improvements.
- Use the chat feature to clarify complex code segments and share insights with your team.
- Promote teamwork by sharing code snippets and explanations using the integrated features.
- Personalize Cody's settings based on your workflow preferences for the best performance.