---
title: "Include Code Samples for Context-Aware Suggestions"
description: "Provide existing code samples to get more relevant LLM suggestions"
category: "tips-tricks"
tags: ["prompting", "code-samples", "context", "llm", "suggestions"]
tech_stack: ["any"]
---

To make your interactions with a language model (LLM) more effective, include code samples from your own projects when you ask for help. This approach gives the LLM a better understanding of your coding style and context, resulting in more relevant recommendations.

Here’s how to do it:

1. **Find the right code snippets** that showcase your coding style or the specific areas where you need assistance.
2. **Format your request** to the LLM by adding these snippets. For example:
   ```
   Here’s a function I’m working on:
   ```python
   def calculate_area(radius):
       return 3.14 * radius * radius
   ```
   Can you suggest improvements or alternatives?
   ```
3. **Send your request** to the LLM with the formatted prompt.
4. **Look over the suggestions** the LLM provides, and see how well they fit with your existing code.
5. **Use any helpful suggestions** in your codebase, making adjustments as needed.

Expected outcome: You’ll receive suggestions that are more relevant and tailored to your coding style.

### Why This Works
By including code samples, you give the LLM context. This context allows it to offer suggestions that align better with your current code structure and style. Use this method when looking for improvements, alternatives, or help with debugging.

### Quick Examples
- **Before**: 
   ```
   Can you help me optimize my function?
   ```
- **After**: 
   ```
   Here’s my function:
   ```python
   def fetch_data(api_url):
       response = requests.get(api_url)
       return response.json()
   ```
   What optimizations can I make?
   ```
- **Expected Improvement**: You’ll get more specific suggestions aimed at improving the `fetch_data` function.

- **Before**: 
   ```
   How do I handle errors in my code?
   ```
- **After**: 
   ```
   Here’s my error handling:
   ```python
   try:
       result = risky_operation()
   except Exception as e:
       print(e)
   ```
   What’s a better way to handle this?
   ```

### Common Mistakes
- **Not providing enough context**: Vague requests can lead to less helpful responses. Always include relevant code snippets.
  
- **Using outdated code samples**: Make sure your code reflects your current practices. Regularly update the snippets you share.

- **Overloading with too much code**: Too much code can confuse the LLM. Stick to 2-3 concise snippets that are directly related to your question.

- **Ignoring LLM suggestions**: Dismissing suggestions without testing them can cause you to miss out on valuable insights. Experiment with the suggestions before deciding against them.