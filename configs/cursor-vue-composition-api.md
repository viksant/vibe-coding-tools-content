---
title: "Cursor Vue.js Composition API"
description: "Optimizes Cursor configuration for Vue.js 3+ development with Composition API, Pinia state management, and TypeScript."
category: "configuration"
tags: ["cursor", "vuejs", "composition-api", "pinia", "typescript", "vue3", "vite"]
tech_stack: ["vue", "typescript", "pinia", "vite", "nuxt"]
---

This setup tailors Cursor for Vue.js 3+ development, particularly with the Composition API, Pinia for state management, and TypeScript integration.

### Configuration Overview
With this configuration, you create a solid environment for developing Vue.js applications that leverage the Composition API. You'll manage state through Pinia, enjoy TypeScript support, and rely on Vite as your build tool.

### Prerequisites
Before you begin, make sure you have:
- Node.js (version 14 or later)
- npm or Yarn (your package manager)
- The latest version of Cursor IDE

### Installation & Setup
Let's get your project up and running:

1. **Create a new Vue.js project**:
   ```bash
   npm create vite@latest my-vue-app --template vue-ts
   cd my-vue-app
   ```
2. **Install Pinia**:
   ```bash
   npm install pinia
   ```
3. **Open the project in Cursor IDE**:
   ```bash
   cursor open my-vue-app
   ```
4. **Configure Pinia in your application**:
   - Inside `src/main.ts`, add the following code:
   ```typescript
   import { createApp } from 'vue';
   import { createPinia } from 'pinia';
   import App from './App.vue';

   const app = createApp(App);
   app.use(createPinia());
   app.mount('#app');
   ```

### File Structure
Here's how your project should look:
```
my-vue-app/
├── public/
│   └── index.html
├── src/
│   ├── assets/
│   ├── components/
│   ├── stores/
│   │   └── myStore.ts
│   ├── App.vue
│   ├── main.ts
├── package.json
├── tsconfig.json
└── vite.config.ts
```

### Key Configuration Files
- **`package.json`**:
```json
{
  "name": "my-vue-app",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "serve": "vite preview"
  },
  "dependencies": {
    "vue": "^3.2.0",
    "pinia": "^2.0.0"
  },
  "devDependencies": {
    "vite": "^2.0.0",
    "typescript": "^4.0.0"
  }
}
```
- **`vite.config.ts`**:
```typescript
import { defineConfig } from 'vite';
import vue from '@vitejs/plugin-vue';

export default defineConfig({
  plugins: [vue()],
  server: {
    port: 3000,
    open: true
  }
});
```

### Advanced Options
You can take your configuration a step further:
- **Enable TypeScript strict mode**: In `tsconfig.json`, set `"strict": true` to enhance type safety.
- **Optimize dependencies**: Run `vite optimize` to pre-bundle dependencies for quicker builds.

### Troubleshooting
Here are some common issues you might face:
- **Issue: Vite server not starting**: Make sure Node.js is installed and check for the correct version. Look for any errors in your terminal.
- **Issue: Pinia store not recognized**: Double-check that you imported and used Pinia correctly in `main.ts`.

### Best Practices
To keep your project organized:
- **Component Organization**: Create small, focused components. Use the Composition API to manage state and lifecycle hooks effectively.
- **State Management**: Rely on Pinia for global state management, and avoid prop drilling by leveraging stores.

### Performance Tuning
Finally, here are some tips for better performance:
- **Lazy Loading**: Use dynamic imports for components to speed up initial load times.
- **Production Build**: Always run `npm run build` before deploying to ensure you serve optimized assets.