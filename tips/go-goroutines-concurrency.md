---
title: "Request Go Goroutines for Concurrency"
description: "Get efficient concurrent Go code using goroutines and channels"
category: "tips-tricks"
tags: ["go", "goroutines", "concurrency", "channels", "golang"]
tech_stack: ["go"]
---

To write concurrent Go code that works well, you can use **goroutines** and **channels**. This setup lets your application handle multiple tasks at once, making it more responsive and faster.

First, let’s define a function you want to run concurrently. Here’s a simple example:

```go
func fetchData(url string) (string, error) {
    // Simulate fetching data
    return "data from " + url, nil
}
```

Next, create a channel to get results from your goroutines:

```go
results := make(chan string)
```

Now, launch a goroutine to run your function concurrently:

```go
go func() {
    data, err := fetchData("http://example.com")
    if err == nil {
        results <- data
    }
}()
```

After that, you can receive results from the channel:

```go
result := <-results
fmt.Println(result)
```

Don't forget to handle errors by checking the return values in your goroutine.

### Why This Works
This method taps into Go's concurrency model, which allows multiple tasks to run at the same time without slowing down the main thread. Use this approach when you’re performing I/O operations, like fetching data from several sources, or when you want your application to respond more quickly.

### Quick Examples
Let's look at a couple of quick examples to illustrate this.

**Example 1: Fetching multiple URLs**
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

**Example 2: Concurrent computation**
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

### Common Mistakes
Here are some pitfalls to watch out for:

- **Not handling errors**: Always check for errors in your goroutines.
  - **Fix**: Make sure to include error handling in your goroutine.

- **Blocking on channels**: Forgetting to read from channels can lead to deadlocks.
  - **Fix**: Read from channels promptly after sending data.

- **Using shared variables without synchronization**: This can create race conditions.
  - **Fix**: Use channels for communication between goroutines instead of shared variables.

- **Not using `sync.WaitGroup`**: This might cause your program to terminate too early.
  - **Fix**: Use `sync.WaitGroup` to wait for all goroutines to finish before the program exits.