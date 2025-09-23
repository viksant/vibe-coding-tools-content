---
title: "Claude Code PHP Laravel"
description: "Configures a robust PHP Laravel environment with Eloquent ORM, Blade templating, and RESTful API capabilities."
category: "configuration"
tags: ["claude-code", "php", "laravel", "eloquent", "blade", "api", "middleware", "database", "queue"]
tech_stack: ["php", "laravel", "mysql", "composer", "artisan", "livewire", "php8"]
---

This configuration sets up a robust PHP Laravel environment with Eloquent ORM, Blade templating, and RESTful API capabilities.

### Configuration Overview
This setup enables efficient development using Laravel's features, including Eloquent ORM for database interactions, Blade for templating, and RESTful API design for web services.

### Prerequisites
- **PHP**: Version 8.0 or higher
- **Composer**: Latest version for dependency management
- **MySQL**: Version 5.7 or higher
- **Node.js**: For asset compilation (optional)
- **Laravel**: Install via Composer

### Installation & Setup
1. **Install Composer**:
   ```bash
   curl -sS https://getcomposer.org/installer | php
   sudo mv composer.phar /usr/local/bin/composer
   ```
2. **Create a new Laravel project**:
   ```bash
   composer create-project --prefer-dist laravel/laravel my-laravel-app
   ```
3. **Navigate to your project directory**:
   ```bash
   cd my-laravel-app
   ```
4. **Set up your environment file**:
   - Copy the `.env.example` to `.env`:
   ```bash
   cp .env.example .env
   ```
   - Update database credentials in the `.env` file:
   ```env
   DB_CONNECTION=mysql
   DB_HOST=127.0.0.1
   DB_PORT=3306
   DB_DATABASE=your_database
   DB_USERNAME=your_username
   DB_PASSWORD=your_password
   ```
5. **Generate the application key**:
   ```bash
   php artisan key:generate
   ```
6. **Run migrations**:
   ```bash
   php artisan migrate
   ```
7. **Serve the application**:
   ```bash
   php artisan serve
   ```

### File Structure
```
my-laravel-app/
├── app/
│   ├── Http/
│   │   ├── Controllers/
│   │   └── Middleware/
│   ├── Models/
│   └── ...
├── config/
├── database/
│   ├── migrations/
│   └── seeders/
├── resources/
│   ├── views/
│   └── js/
├── routes/
├── storage/
└── tests/
```

### Key Configuration Files
- **`.env`**: Environment variables for database and application settings.
- **`config/app.php`**: Main configuration file for application settings.
- **`routes/web.php`**: Define web routes here.
- **`routes/api.php`**: Define API routes here.

### Advanced Options
- **Middleware for Authentication**: Use Laravel's built-in middleware for user authentication.
- **Queue Jobs**: Configure queues for handling background tasks by setting up a queue driver in `.env`:
```env
QUEUE_CONNECTION=database
```
- **Caching Configuration**: Optimize performance by caching configuration and routes:
```bash
php artisan config:cache
php artisan route:cache
```

### Troubleshooting
- **Database Connection Issues**: Ensure the database server is running and credentials in `.env` are correct.
- **Migration Errors**: Check for existing tables or incorrect migration files.
- **Asset Compilation Issues**: If using Laravel Mix, ensure Node.js and npm are installed, and run:
```bash
npm install
npm run dev
```

### Best Practices
- **Version Control**: Use Git for version control and manage your codebase effectively.
- **Environment Management**: Use separate `.env` files for local and production environments.
- **Testing**: Write tests for your application using Laravel's built-in testing features.
- **Documentation**: Maintain clear documentation for your API endpoints and application architecture.

### Performance Tuning
- **Optimize Autoloader**: Use Composer's optimized autoloader:
```bash
composer install --optimize-autoloader --no-dev
```
- **Database Indexing**: Ensure proper indexing on database tables to speed up queries.
- **Use Redis or Memcached**: For caching and session storage to improve performance.