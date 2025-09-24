---
title: "AutoHotkey v2 Coding Guidelines"
description: "As a leading expert in AutoHotkey v2, you will consistently deliver code that is both concise and comprehensible. The following guidelines will direct your scripting practices."
category: "rules"
tags: ["AutoHotkey", "scripting", "best practices"]
tech_stack: ["AutoHotkey v2"]
---

You have a solid grasp of AutoHotkey v2 scripting. Your goal is to consistently write code that is clear and easy to understand. Let’s explore some guidelines to help you sharpen your scripting skills:

- **API Approach**: Whenever possible, lean on API methods rather than mimicking human actions. For instance, try to avoid using mouse clicks and keystrokes.

- **Naming Conventions**: Stick to camel case for naming all your variables, functions, and classes. Aim for names that are between 5 and 25 characters long, and ensure they clearly describe their purpose.

- **No External Dependencies**: Keep your scripts self-contained. Avoid relying on external libraries or dependencies.

- **Function Ownership**: Make sure you implement every function you define. This practice not only ensures originality but also adds clarity to your code.

- **Script Structure**: Organize your script by placing all function and class definitions at the end. This layout makes for a cleaner and more manageable script.

- **Inline Comments**: Don’t forget to include inline comments to explain your code’s functionality. This helps beginner programmers understand your logic.

- **Simplicity Over Complexity**: Focus on writing simpler scripts, even if that means they are longer. Only opt for complex solutions when they substantially improve performance.

- **Brace Style**: Use the One True Brace style for your functions, classes, loops, and if statements. This will make your code more readable.

**Script Header**: Start each script with these lines:

```ahk
#Requires AutoHotkey v2.0.2+
#SingleInstance Force ; Limit one running version of this script
DetectHiddenWindows true ; Ensure hidden windows can be found
ListLines True ; Enables debugging of the script (default is on)
SetWorkingDir A_InitialWorkingDir ; Set the working directory to the script's directory
```

**Hotkeys**: After the AutoExecute section of your script, include these hotkeys:

```ahk
^+e::Edit ; Control+Shift+E to edit the current script
^+Escape::Exitapp ; Control+Shift+Escape will exit the app
^+r::Reload ; Reload the current script
```

By following these guidelines, you’ll write scripts that are not only functional but also easy for others to read and maintain. Happy scripting!