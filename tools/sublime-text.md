---
title: "Sublime Text"
description: "A high-performance text editor with advanced features like multiple selections, command palette, and goto anything functionality, known for speed and responsiveness with extensive customization through packages and themes."
category: "tools"
tags: ["text-editor", "performance", "plugins", "multiple-selections", "goto-anything", "cross-platform"]
tech_stack: ["any", "web-development", "programming", "markup-languages"]
---

### Tool Benefits
Sublime Text is a sophisticated text editor that provides developers with a fast and responsive environment for coding. Key benefits include:
- **Speed and Performance**: Sublime Text is optimized for performance, allowing for quick file opening and editing, even with large files.
- **Multiple Selections**: Edit multiple lines simultaneously, enhancing productivity and reducing repetitive tasks.
- **Goto Anything**: Quickly navigate to files, symbols, or lines within your project using a simple keyboard shortcut.
- **Extensive Plugin Ecosystem**: Customize your editor with a wide range of packages and themes available through Package Control.
- **Powerful Search and Replace**: Utilize regex support for advanced search and replace functionality across files.

### Setup & Installation
#### Windows
1. Download the installer from the [Sublime Text website](https://www.sublimetext.com/).
2. Run the installer and follow the prompts to complete the installation.
3. Launch Sublime Text from the Start menu or desktop shortcut.

#### macOS
1. Download the `.dmg` file from the [Sublime Text website](https://www.sublimetext.com/).
2. Open the `.dmg` file and drag Sublime Text to the Applications folder.
3. Launch Sublime Text from the Applications folder or Spotlight.

#### Linux
1. For Ubuntu, run the following commands in the terminal:
   ```bash
   sudo apt update
   sudo apt install sublime-text
   ```
2. For other distributions, follow the instructions on the [Sublime Text Linux installation page](https://www.sublimetext.com/docs/linux_repositories.html).

### Configuration
- **User Preferences**: Access user preferences by navigating to `Preferences > Settings`. Here you can customize settings such as:
  ```json
  {
    "font_size": 12,
    "theme": "Default.sublime-theme",
    "ignored_packages": ["Vintage"]
  }
  ```
- **Package Control**: Install Package Control to manage plugins easily. Open the command palette with `Ctrl + Shift + P` and type `Install Package Control`.

### Usage Guide
- **Creating a New File**: Press `Ctrl + N` to create a new file.
- **Opening a File**: Use `Ctrl + O` to open an existing file.
- **Using Goto Anything**: Press `Ctrl + P`, then start typing the file name or line number to quickly navigate.
- **Multiple Selections**: Hold `Ctrl` (or `Cmd` on macOS) and click to create multiple cursors, allowing simultaneous editing.

### Advanced Features
- **Snippets**: Create reusable code snippets by saving them in a `.sublime-snippet` file. Example:
  ```xml
  <snippet>
    <content><![CDATA[
    function ${1:functionName}(${2:args}) {
        ${3:// body}
    }
    ]]></content>
    <tabTrigger>func</tabTrigger>
    <scope>source.js</scope>
  </snippet>
  ```
- **Build Systems**: Create custom build systems by navigating to `Tools > Build System > New Build System`. Example for Python:
  ```json
  {
    "cmd": ["python3", "-u", "$file"],
    "selector": "source.python"
  }
  ```
- **Keyboard Shortcuts**: Customize keyboard shortcuts by editing the `Key Bindings` in `Preferences > Key Bindings`.

### Troubleshooting
- **Plugin Issues**: If Sublime Text crashes, try starting in safe mode by running `sublime_text --safe-mode` in the terminal.
- **File Encoding Problems**: If you encounter encoding issues, check the encoding settings in `File > Reopen with Encoding`.
- **Performance Lag**: Disable unused plugins by going to `Preferences > Package Control > Disable Package`.

### Best Practices
- **Regularly Update Sublime Text**: Keep your installation up to date for the latest features and bug fixes.
- **Use Version Control**: Integrate Sublime Text with Git or other version control systems for better project management.
- **Organize Projects**: Use project files to manage multiple files and folders efficiently. Create a project by selecting `Project > Save Project As`.
- **Leverage the Command Palette**: Familiarize yourself with the command palette for quick access to commands and settings. Press `Ctrl + Shift + P` to open it.