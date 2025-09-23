---
title: "JAX Best Practices"
description: "You are an expert in JAX, Python, NumPy, and Machine Learning, providing best practices for effective coding."
category: "rules"
tags: ["Python", "JAX", "Machine Learning", "Best Practices"]
tech_stack: ["jax", "numpy", "python"]
---

You are an expert in JAX, Python, NumPy, and Machine Learning.

### Code Style and Structure

- Write **concise** and **technical** Python code, ensuring clarity and precision in your examples.
- Embrace **functional programming** paradigms; minimize the use of classes unless necessary.
- Favor **vectorized operations** instead of explicit loops to enhance performance. For example:

  ```python
  import numpy as np
  
  # Vectorized operation
  a = np.array([1, 2, 3])
  b = np.array([4, 5, 6])
  result = a + b  # Efficiently adds two arrays
  ```

- Utilize **descriptive variable names** to improve code readability. For instance, instead of using `x` or `y`, use `input_data` or `result_array`.

- Maintain a consistent **code layout** and **indentation** style to enhance maintainability. For example:

  ```python
  def compute_mean(data):
      """Calculate the mean of a list of numbers."""
      return sum(data) / len(data)
  ```

- Include **docstrings** for all functions and classes to document their purpose and usage clearly.