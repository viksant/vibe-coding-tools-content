---
title: "Request Rust Memory Safety Patterns"
description: "Get safe Rust code with proper ownership and borrowing patterns"
category: "tips-tricks"
tags: ["rust", "memory-safety", "ownership", "borrowing", "zero-cost"]
tech_stack: ["rust"]
---

To ensure your Rust code is memory safe, focus on proper **ownership** and **borrowing** patterns. This approach helps prevent data races and dangling references, leading to more reliable applications. Follow these steps to request safe Rust code:

1. **Specify Ownership Requirements**: Clearly state the ownership rules for your variables.
   - Example: "Please ensure that the variable `x` is owned by the function and not passed by reference."

2. **Request Borrowing Rules**: Ask for explicit borrowing patterns to avoid mutable aliasing.
   - Example: "Use immutable references for reading and mutable references only when necessary."

3. **Include Lifetime Annotations**: If your code involves complex references, request lifetime annotations.
   - Example: "Add lifetime annotations to ensure references do not outlive their data."

4. **Ask for Zero-Cost Abstractions**: Emphasize the need for performance without sacrificing safety.
   - Example: "Use iterators and other zero-cost abstractions where applicable."

5. **Review for Memory Safety**: Finally, ask for a review of the code to ensure it adheres to Rust’s memory safety guarantees.
   - Example: "Can you verify that there are no potential data races or dangling references?"

Expected result: You will receive Rust code that adheres to ownership, borrowing, and memory safety principles.

### Why It Works
This approach leverages Rust's unique ownership model to enforce memory safety at compile time, reducing runtime errors. Use it when writing or reviewing Rust code, especially in concurrent applications.

### Quick Examples
- **Before**: 
  ```rust
  fn example(x: &i32) {
      let y = x; // Potential dangling reference
  }
  ```
- **After**: 
  ```rust
  fn example(x: i32) {
      let y = x; // Proper ownership
  }
  ```

- **Before**: 
  ```rust
  fn read_data(data: &mut Vec<i32>) {
      let ref1 = &data[0]; // Mutable aliasing
  }
  ```
- **After**: 
  ```rust
  fn read_data(data: &Vec<i32>) {
      let ref1 = &data[0]; // Immutable borrow
  }
  ```

### Common Mistakes
- **Mistake**: Forgetting to specify ownership, leading to confusion.
  - **Fix**: Always clarify ownership in your requests.
  
- **Mistake**: Using mutable references without justification.
  - **Fix**: Only use mutable references when necessary and document why.

- **Mistake**: Overlooking lifetime annotations in complex scenarios.
  - **Fix**: Include lifetime requirements in your requests for clarity.

- **Mistake**: Ignoring performance implications of abstractions.
  - **Fix**: Request zero-cost abstractions explicitly to ensure efficiency.