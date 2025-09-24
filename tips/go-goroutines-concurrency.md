---
title: "Request Go Goroutines for Concurrency"
description: "Get efficient concurrent Go code using goroutines and channels"
category: "tips-tricks"
tags: ["go", "goroutines", "concurrency", "channels", "golang"]
tech_stack: ["go"]
---

To write efficient concurrent Go code, utilize **goroutines** and **channels** for managing tasks concurrently. This approach allows your application to handle multiple operations simultaneously, improving performance and responsiveness.

1. **Define a function** that you want to run concurrently. For example:
   ```go
   func fetchData(url string) (string, error) {
       // Simulate fetching data
       return "data from " + url, nil
   }
   ```
2. **Create a channel** to receive results from goroutines:
   ```go
   results := make(chan string)
   ```
3. **Launch goroutines** to execute your function concurrently:
   ```go
   go func() {
       data, err := fetchData("http://example.com")
       if err == nil {
           results <- data
       }
   }()
   ```
4. **Receive results** from the channel:
   ```go
   result := <-results
   fmt.Println(result)
   ```
5. **Handle errors** appropriately by checking the return values in your goroutine.

Expected result: You will efficiently fetch data concurrently and handle results through channels.

### WHY IT WORKS
This method leverages Go's concurrency model, allowing multiple tasks to run simultaneously without blocking the main thread. Use it when you need to perform I/O operations, like fetching data from multiple sources, or when you want to improve application responsiveness.

### QUICK EXAMPLES
- **Example 1: Fetching multiple URLs**
  ```go
  urls := []string{"http://example1.com", "http://example2.com"}
  results := make(chan string)
  for _, url := range urls {
      go func(u string) {
          data, _ := fetchData(u)
          results <- data
      }(url)
  }
  for range urls {
      fmt.Println(<-results)
  }
  ```
- **Example 2: Concurrent computation**
  ```go
  nums := []int{1, 2, 3}
  results := make(chan int)
  for _, num := range nums {
      go func(n int) {
          results <- n * n
      }(num)
  }
  for range nums {
      fmt.Println(<-results)
  }
  ```

### COMMON MISTAKES
- **Not handling errors**: Always check for errors in goroutines.
  - **Fix**: Include error handling in your goroutine.
  
- **Blocking on channels**: Forgetting to read from channels can cause deadlocks.
  - **Fix**: Ensure you read from channels as soon as data is sent.

- **Using shared variables without synchronization**: This can lead to race conditions.
  - **Fix**: Use channels to communicate between goroutines instead of shared variables.

- **Not using `sync.WaitGroup`**: This can lead to premature program termination.
  - **Fix**: Use `sync.WaitGroup` to wait for all goroutines to finish before exiting.