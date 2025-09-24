---
title: "GitHub Copilot Progressive Web Apps"
description: "Configures GitHub Copilot for PWA development with service workers and offline capabilities."
category: "configuration"
tags: ["github-copilot", "pwa", "service-workers", "offline", "web-app", "manifest"]
tech_stack: ["javascript", "service-workers", "workbox", "manifest", "cache-api", "push-notifications"]
---

This guide helps you set up GitHub Copilot for developing Progressive Web Apps (PWAs). You'll learn how to enable service workers and offline capabilities, making your web app experience feel more like a native app.

### Configuration Overview
With this setup, you can create PWAs using GitHub Copilot. It includes service workers, offline strategies, and push notifications to enhance user experience.

### Prerequisites
Before you get started, make sure you have these installed:
- **Node.js**: Version 14 or higher
- **npm**: Version 6 or higher
- **GitHub Copilot**: Enabled in your IDE (VSCode is a great choice)
- A basic understanding of JavaScript and web development

### Installation & Setup
Let’s walk through the setup steps together.

1. **Create a new project directory**:
   ```bash
   mkdir my-pwa-app
   cd my-pwa-app
   ```

2. **Initialize a new Node.js project**:
   ```bash
   npm init -y
   ```

3. **Install required dependencies**:
   ```bash
   npm install workbox-cli --save-dev
   ```

4. **Create essential files**:
   You’ll need the following files:
   - `index.html`
   - `manifest.json`
   - `service-worker.js`
   - A `src/` directory for additional scripts

5. **Set up your `index.html`**:
   Here’s a simple HTML setup to get you started:
   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <link rel="manifest" href="manifest.json">
       <title>My PWA App</title>
   </head>
   <body>
       <h1>Hello, PWA!</h1>
       <script src="service-worker.js"></script>
   </body>
   </html>
   ```

6. **Configure `manifest.json`**:
   This file helps define your PWA's settings:
   ```json
   {
       "name": "My PWA App",
       "short_name": "PWA",
       "start_url": ".",
       "display": "standalone",
       "background_color": "#ffffff",
       "theme_color": "#000000",
       "icons": [
           {
               "src": "icon-192x192.png",
               "sizes": "192x192",
               "type": "image/png"
           },
           {
               "src": "icon-512x512.png",
               "sizes": "512x512",
               "type": "image/png"
           }
       ]
   }
   ```

7. **Implement `service-worker.js`**:
   Here’s a basic service worker setup:
   ```javascript
   self.addEventListener('install', (event) => {
       console.log('Service Worker: Installed');
   });

   self.addEventListener('activate', (event) => {
       console.log('Service Worker: Activated');
   });

   self.addEventListener('fetch', (event) => {
       console.log('Service Worker: Fetching', event.request.url);
   });
   ```

8. **Build the service worker using Workbox**:
   Run this command to generate the service worker:
   ```bash
   npx workbox generateSW workbox-config.js
   ```

### File Structure
Your project should look like this:
```
my-pwa-app/
├── index.html
├── manifest.json
├── service-worker.js
├── workbox-config.js
└── src/
    └── additional-scripts.js
```

### Key Configuration Files
- **`workbox-config.js`**: This file configures Workbox for caching and generating your service worker.
  ```javascript
  module.exports = {
      globDirectory: 'dist/',
      globPatterns: ['**/*.{html,js,css,png,jpg}'],
      swDest: 'dist/service-worker.js',
      runtimeCaching: [{
          urlPattern: new RegExp('^https://your-api-url/'),
          handler: 'NetworkFirst'
      }]
  };
  ```

### Advanced Options
Consider adding these features:
- **Background Sync**: This lets your app handle requests when the network is available.
- **Push Notifications**: Subscribe users and manage push events in your service worker.

### Troubleshooting
If you run into issues, here are some tips:
- **Service Worker not registering**: Check the service worker file path and ensure it’s served over HTTPS.
- **Caching issues**: Clear your browser cache or unregister the service worker to see changes.
- **Manifest not loading**: Make sure the path in the `<link rel="manifest">` tag is correct and that your JSON is valid.

### Best Practices
Keep these in mind:
- Always use **HTTPS** for your PWA resources.
- Regularly update your dependencies for security.
- Test on different devices and browsers for compatibility and performance.

### Performance Optimizations
Here are some ways to improve performance:
- Use **Workbox** for smart caching strategies.
- Minimize your JavaScript and CSS to speed up load times.
- Implement lazy loading for images and assets to enhance initial load performance.