---
title: "GitHub Copilot Progressive Web Apps"
description: "Configures GitHub Copilot for PWA development with service workers and offline capabilities."
category: "configuration"
tags: ["github-copilot", "pwa", "service-workers", "offline", "web-app", "manifest"]
tech_stack: ["javascript", "service-workers", "workbox", "manifest", "cache-api", "push-notifications"]
---

This configuration sets up GitHub Copilot for Progressive Web App (PWA) development, enabling service workers and offline capabilities.

### Configuration Overview
This setup facilitates the development of Progressive Web Apps using GitHub Copilot, incorporating service workers, offline-first strategies, and push notifications to create app-like experiences.

### Prerequisites
- **Node.js**: Version 14 or higher
- **npm**: Version 6 or higher
- **GitHub Copilot**: Enabled in your IDE (VSCode recommended)
- **Basic knowledge of JavaScript and web development**

### Installation & Setup
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
   - `index.html`
   - `manifest.json`
   - `service-worker.js`
   - `src/` directory for additional scripts

5. **Set up your `index.html`**:
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
   ```bash
   npx workbox generateSW workbox-config.js
   ```

### File Structure
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
- **`workbox-config.js`**: Configuration for Workbox to manage caching and service worker generation.
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
- **Background Sync**: Implement background sync to handle requests when the network is available.
- **Push Notifications**: Integrate push notifications by subscribing users and handling push events in the service worker.

### Troubleshooting
- **Service Worker not registering**: Ensure that the service worker file path is correct and served over HTTPS.
- **Caching issues**: Clear the browser cache or unregister the service worker to test changes.
- **Manifest not loading**: Verify the path in the `<link rel="manifest">` tag and check for valid JSON format.

### Best Practices
- Use **HTTPS** for all PWA resources.
- Regularly update dependencies to keep up with security patches.
- Test on multiple devices and browsers to ensure compatibility and performance.

### Performance Optimizations
- Utilize **Workbox** for efficient caching strategies.
- Minimize JavaScript and CSS files to reduce load times.
- Implement lazy loading for images and assets to improve initial load performance.