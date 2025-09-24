---
title: "Include Code Samples for Context-Aware Suggestions"
description: "Provide existing code samples to get more relevant LLM suggestions"
category: "tips-tricks"
tags: ["prompting", "code-samples", "context", "llm", "suggestions"]
tech_stack: ["any"]
---

To enhance the relevance of suggestions from a language model (LLM), include code samples from your existing codebase when making requests. This practice helps the LLM understand your coding style and context, leading to more tailored recommendations. 

1. **Identify the relevant code snippets** that represent your coding style or the specific area you need help with.
2. **Format your request** to the LLM by including these snippets. For example:
   ```
   Here’s a function I’m working on:
   ```python
   def calculate_area(radius):
       return 3.14 * radius * radius
   ```
   Can you suggest improvements or alternatives?
   ```
3. **Submit your request** to the LLM using the formatted prompt.
4. **Review the suggestions** provided by the LLM, focusing on how they align with your existing code.
5. **Incorporate useful suggestions** into your codebase, adapting them as necessary.

Expected result: You will receive more relevant and context-aware suggestions that fit your coding style.

### Why It Works
Including code samples provides the LLM with context, allowing it to generate suggestions that are more aligned with your existing code structure and style. Use this approach when seeking improvements, alternatives, or debugging help.

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
- **Expected Improvement**: More specific suggestions tailored to the `fetch_data` function.

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
- **Not providing enough context**: Avoid vague requests. Include relevant code snippets.
  - **Fix**: Always add code that illustrates your current implementation.
  
- **Using outdated code samples**: Ensure the code reflects your current practices.
  - **Fix**: Regularly update the snippets you share with the LLM.

- **Overloading with too much code**: Including excessive code can confuse the LLM.
  - **Fix**: Limit to 2-3 concise snippets that are directly relevant to your question.

- **Ignoring LLM suggestions**: Dismissing suggestions without testing can miss valuable insights.
  - **Fix**: Experiment with the suggestions before deciding against them.