---
title: "Cursor Vue.js Composition API"
description: "Optimizes Cursor configuration for Vue.js 3+ development with Composition API, Pinia state management, and TypeScript."
category: "configuration"
tags: ["cursor", "vuejs", "composition-api", "pinia", "typescript", "vue3", "vite"]
tech_stack: ["vue", "typescript", "pinia", "vite", "nuxt"]
---

This configuration optimizes Cursor for Vue.js 3+ development with Composition API, Pinia state management, and TypeScript integration.

### Configuration Overview
This setup provides a robust development environment for building Vue.js applications using the Composition API, with state management via Pinia, TypeScript support, and Vite as the build tool.

### Prerequisites
- Node.js (version 14 or later)
- npm or Yarn (package manager)
- Cursor IDE (latest version)

### Installation & Setup
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
   - In `src/main.ts`, add:
   ```typescript
   import { createApp } from 'vue';
   import { createPinia } from 'pinia';
   import App from './App.vue';

   const app = createApp(App);
   app.use(createPinia());
   app.mount('#app');
   ```

### File Structure
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
- **Enable TypeScript strict mode**: In `tsconfig.json`, set `"strict": true` for better type safety.
- **Optimize dependencies**: Use `vite optimize` to pre-bundle dependencies for faster builds.

### Troubleshooting
- **Issue: Vite server not starting**: Ensure Node.js is installed and the correct version is being used. Check for errors in the terminal.
- **Issue: Pinia store not recognized**: Verify that Pinia is correctly imported and used in `main.ts`.

### Best Practices
- **Component Organization**: Keep components small and focused. Use the Composition API to manage state and lifecycle hooks effectively.
- **State Management**: Use Pinia for global state management and avoid prop drilling by leveraging stores.

### Performance Tuning
- **Lazy Loading**: Implement dynamic imports for components to improve initial load time.
- **Production Build**: Always run `npm run build` before deploying to ensure optimized assets are served.