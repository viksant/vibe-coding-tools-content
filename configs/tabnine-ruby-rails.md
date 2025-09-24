---
title: "Tabnine Ruby on Rails"
description: "Configures Tabnine for Ruby on Rails development with ActiveRecord, RESTful routing, and MVC architecture."
category: "configuration"
tags: ["tabnine", "ruby", "rails", "activerecord", "mvc", "restful", "sidekiq", "rspec"]
tech_stack: ["ruby", "rails", "postgresql", "redis", "rspec", "sidekiq"]
---

This configuration helps you get the most out of Tabnine for Ruby on Rails development, especially when working with ActiveRecord, RESTful routing, and the MVC architecture.

### Configuration Overview
This setup streamlines Ruby on Rails development by integrating Tabnine for smart code completion. It makes use of ActiveRecord for object-relational mapping, implements RESTful routing, and employs Sidekiq for handling background jobs.

### Prerequisites
Before diving in, make sure you have the following:

- **Ruby**: Version 3.0 or higher
- **Rails**: Version 6.0 or higher
- **PostgreSQL**: Version 12 or higher
- **Redis**: Version 6.0 or higher
- **RSpec**: Version 3.10 or higher
- **Sidekiq**: Version 6.2 or higher
- **Tabnine**: Latest version installed in your IDE

### Installation & Setup
Let’s get your environment ready:

1. **Install Ruby and Rails**:
   ```bash
   gem install rails
   ```
2. **Create a new Rails application**:
   ```bash
   rails new myapp --database=postgresql
   cd myapp
   ```
3. **Add the required gems to your `Gemfile`**:
   ```ruby
   gem 'pg'
   gem 'sidekiq'
   gem 'rspec-rails', group: [:development, :test]
   gem 'tabnine'
   ```
4. **Install the gems**:
   ```bash
   bundle install
   ```
5. **Set up RSpec**:
   ```bash
   rails generate rspec:install
   ```
6. **Configure Sidekiq**:
   Create a file called `config/initializers/sidekiq.rb`:
   ```ruby
   Sidekiq.configure_server do |config|
     config.redis = { url: 'redis://localhost:6379/0' }
   end

   Sidekiq.configure_client do |config|
     config.redis = { url: 'redis://localhost:6379/0' }
   end
   ```
7. **Set up Tabnine**:
   - Install the Tabnine plugin in your IDE (like VSCode or RubyMine).
   - Adjust Tabnine settings to fit your style.

### File Structure
Here's how your project should look:

```
myapp/
├── app/
│   ├── controllers/
│   ├── models/
│   ├── views/
├── config/
│   ├── initializers/
│   ├── routes.rb
├── db/
│   ├── migrate/
├── spec/
│   ├── models/
│   ├── controllers/
├── Gemfile
├── Gemfile.lock
```

### Key Configuration Files
- **`Gemfile`**:
  ```ruby
  source 'https://rubygems.org'
  gem 'rails', '~> 6.1.0'
  gem 'pg'
  gem 'redis'
  gem 'sidekiq'
  gem 'rspec-rails', group: [:development, :test]
  gem 'tabnine'
  ```
- **`config/routes.rb`**:
  ```ruby
  Rails.application.routes.draw do
    resources :posts
    mount Sidekiq::Web => '/sidekiq'
  end
  ```

### Advanced Options
Want to take it a step further? Here are some tips:

- **Performance Tweaks**:
  - Enable eager loading in production by adding `config.eager_load = true` in `config/environments/production.rb`.
  - Use the `bullet` gem to spot N+1 queries during development.
  
- **Background Job Optimization**:
  - Set up Sidekiq to manage multiple queues for different job priorities.

### Troubleshooting
Facing some issues? Here are common problems and solutions:

- **Issue**: Sidekiq not processing jobs.
  - **Solution**: Check if Redis is running and accessible. Look at Sidekiq logs for any errors.

- **Issue**: RSpec tests failing.
  - **Solution**: Make sure all migrations are current by running `rails db:migrate`.

### Best Practices
Here are some tips for keeping your project in shape:

- Use **RSpec** for all testing to ensure a reliable test suite.
- Keep your **Gemfile** tidy and only include necessary gems.
- Regularly update your gems to gain performance boosts and security fixes.
- Use **environment variables** for sensitive configurations like database credentials.

### Performance Tuning
To get the best performance out of your application:

- Optimize database queries by using `includes` to avoid N+1 issues.
- Keep an eye on Sidekiq performance with the web UI and adjust settings based on your workload.
- Implement caching strategies with Rails caching mechanisms to speed up response times.