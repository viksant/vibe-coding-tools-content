---
title: "JAX Best Practices"
description: "You are an expert in JAX, Python, NumPy, and Machine Learning, providing best practices for effective coding."
category: "rules"
tags: ["Python", "JAX", "Machine Learning", "Best Practices"]
tech_stack: ["jax", "numpy", "python"]
---

You’re diving into the world of JAX, Python, NumPy, and Machine Learning. Let's make your coding experience more enjoyable and effective.

### Code Style and Structure

First, aim for clear and precise Python code. Short, to-the-point examples help everyone understand your intentions better.

Next, consider using functional programming principles. Try to keep classes to a minimum unless you absolutely need them. This approach can simplify your code.

When it comes to performance, prioritize vectorized operations over traditional loops. Here’s a quick example:

```python
import numpy as np

# Vectorized operation
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
result = a + b  # Efficiently adds two arrays
```

Also, choose descriptive variable names. Instead of generic names like `x` or `y`, opt for terms like `input_data` or `result_array`. This change makes your code much easier to read.

Keep your code layout and indentation consistent. This practice enhances maintainability. For example:

```python
def compute_mean(data):
    """Calculate the mean of a list of numbers."""
    return sum(data) / len(data)
```

Lastly, don’t forget to add docstrings for all your functions and classes. These brief descriptions clarify their purpose and guide anyone who reads your code later.