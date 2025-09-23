---
title: "Claude Code Rust Actix Web"
description: "Configures Claude Code for Rust web development with Actix Web, async programming, and database integration."
category: "configuration"
tags: ["claude-code", "rust", "actix-web", "async", "memory-safety", "performance", "web-development"]
tech_stack: ["rust", "actix-web", "tokio", "sqlx", "serde", "diesel", "cargo"]
---

This configuration sets up Claude Code for Rust web development using the Actix Web framework, emphasizing async programming and database integration.

### Configuration Overview
This setup achieves a robust environment for developing high-performance web applications in Rust, leveraging Actix Web for server-side logic and SQLx for database interactions.

### Prerequisites
- **Rust**: Ensure Rust is installed (version 1.56 or higher).
- **Cargo**: Comes with Rust; used for package management.
- **Claude Code**: Installed and configured as your IDE.
- **PostgreSQL**: Database server for SQLx integration.

### Installation & Setup
1. **Install Rust**: 
   ```bash
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
   ```
2. **Create a new Rust project**:
   ```bash
   cargo new my_actix_app
   cd my_actix_app
   ```
3. **Add dependencies**: Update `Cargo.toml` with the following:
   ```toml
   [dependencies]
   actix-web = "4.0"
   tokio = { version = "1", features = ["full"] }
   sqlx = { version = "0.5", features = ["runtime-tokio-rustls", "postgres"] }
   serde = { version = "1.0", features = ["derive"] }
   diesel = { version = "1.4", features = ["postgres"] }
   ```
4. **Create a basic Actix Web server**: In `src/main.rs`, add:
   ```rust
   use actix_web::{web, App, HttpServer, Responder};

   async fn greet() -> impl Responder {
       "Hello, Actix Web!"
   }

   #[actix_web::main]
   async fn main() -> std::io::Result<()> {
       HttpServer::new(|| {
           App::new().route("/", web::get().to(greet))
       })
       .bind("127.0.0.1:8080")?
       .run()
       .await
   }
   ```
5. **Run the application**:
   ```bash
   cargo run
   ```

### File Structure
```
my_actix_app/
├── Cargo.toml
├── src/
│   ├── main.rs
│   └── lib.rs (optional for modular code)
└── migrations/ (for database migrations)
```

### Key Configuration Files
- **`Cargo.toml`**: Defines project dependencies and metadata.
- **`src/main.rs`**: Entry point for the Actix Web application.

### Advanced Options
- **Enable logging**: Add `env_logger` to `Cargo.toml`:
  ```toml
  env_logger = "0.9"
  ```
  Initialize in `main.rs`:
  ```rust
  env_logger::init();
  ```
- **Database connection pooling**: Use SQLx's connection pool for efficient database access.

### Troubleshooting
- **Error: "Could not find crate `actix-web`"**: Ensure dependencies are correctly added to `Cargo.toml` and run `cargo build`.
- **Database connection issues**: Verify PostgreSQL is running and connection settings in your code are correct.

### Best Practices
- **Use environment variables**: Store sensitive data like database URLs in environment variables instead of hardcoding them.
- **Modularize code**: Split functionality into separate modules for better organization and maintainability.

### Performance Tuning
- **Optimize database queries**: Use SQLx's query builder for efficient SQL generation.
- **Enable HTTP/2**: Consider using `actix-web-http2` for better performance in production.

### Workflow Optimization Tips
- **Hot reloading**: Use `cargo watch` to automatically rebuild and run your application on file changes:
  ```bash
  cargo watch -x run
  ```
- **Testing**: Write unit tests for your handlers using Actix's test utilities to ensure reliability.