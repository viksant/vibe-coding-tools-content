---
title: "Tabnine Desktop Electron"
description: "Configures Tabnine for cross-platform desktop app development with Electron, React, and native integrations."
category: "configuration"
tags: ["tabnine", "electron", "desktop", "react", "cross-platform", "native"]
tech_stack: ["electron", "react", "nodejs", "native-modules", "webpack", "typescript"]
---

This configuration sets up a robust Electron desktop application with React UI, native module support, and cross-platform capabilities.

### Configuration Overview
This setup enables the development of cross-platform desktop applications using Electron and React, integrating native modules for enhanced functionality.

### Prerequisites
- **Node.js**: v14 or higher
- **npm**: v6 or higher
- **Electron**: v15 or higher
- **React**: v17 or higher
- **TypeScript**: v4 or higher
- **Webpack**: v5 or higher
- **Tabnine**: Installed and configured

### Installation & Setup
1. **Create a new project directory**:
   ```bash
   mkdir my-electron-app && cd my-electron-app
   ```
2. **Initialize a new Node.js project**:
   ```bash
   npm init -y
   ```
3. **Install required dependencies**:
   ```bash
   npm install electron react react-dom typescript webpack webpack-cli ts-loader
   ```
4. **Set up TypeScript configuration**:
   Create a `tsconfig.json` file:
   ```json
   {
     "compilerOptions": {
       "target": "es5",
       "module": "commonjs",
       "jsx": "react",
       "outDir": "./dist",
       "strict": true
     },
     "include": ["src/**/*"]
   }
   ```
5. **Create the main Electron file**:
   Create a file named `main.ts` in the root directory:
   ```typescript
   import { app, BrowserWindow } from 'electron';
   function createWindow() {
     const win = new BrowserWindow({
       width: 800,
       height: 600,
       webPreferences: {
         nodeIntegration: true,
         contextIsolation: false
       }
     });
     win.loadURL('http://localhost:3000');
   }
   app.whenReady().then(createWindow);
   app.on('window-all-closed', () => {
     if (process.platform !== 'darwin') app.quit();
   });
   app.on('activate', () => {
     if (BrowserWindow.getAllWindows().length === 0) createWindow();
   });
   ```
6. **Set up Webpack configuration**:
   Create a `webpack.config.js` file:
   ```javascript
   const path = require('path');
   module.exports = {
     entry: './src/index.tsx',
     output: {
       filename: 'bundle.js',
       path: path.resolve(__dirname, 'dist')
     },
     resolve: {
       extensions: ['.tsx', '.ts', '.js']
     },
     module: {
       rules: [
         {
           test: /\.tsx?$/,
           use: 'ts-loader',
           exclude: /node_modules/
         }
       ]
     }
   };
   ```
7. **Create the React application entry point**:
   Create a `src/index.tsx` file:
   ```typescript
   import React from 'react';
   import ReactDOM from 'react-dom';
   const App = () => <h1>Hello, Electron with React!</h1>;
   ReactDOM.render(<App />, document.getElementById('root'));
   ```
8. **Add scripts to `package.json`**:
   Modify the `scripts` section:
   ```json
   "scripts": {
     "start": "electron .",
     "build": "webpack"
   }
   ```
9. **Run the application**:
   Build and start the application:
   ```bash
   npm run build
   npm start
   ```

### File Structure
```
my-electron-app/
├── dist/
│   └── bundle.js
├── node_modules/
├── src/
│   └── index.tsx
├── main.ts
├── package.json
├── tsconfig.json
└── webpack.config.js
```

### Key Configuration Files
- **`main.ts`**: Main process for Electron, responsible for creating the application window.
- **`webpack.config.js`**: Configuration for bundling the application with Webpack.
- **`tsconfig.json`**: TypeScript compiler options for the project.

### Advanced Options
- **Auto-Updater**: Integrate `electron-updater` for seamless updates.
- **Native Module Integration**: Use `node-gyp` for building native modules.
- **Performance Optimization**: Enable `webpack` optimization settings for production builds.

### Troubleshooting
- **Issue**: Application fails to start.
  - **Solution**: Ensure all dependencies are installed and check the console for errors.
- **Issue**: Webpack not bundling files.
  - **Solution**: Verify the entry path in `webpack.config.js` and ensure `ts-loader` is installed.

### Best Practices
- **Use Environment Variables**: For configuration settings, use `dotenv` to manage environment variables.
- **Modular Code Structure**: Keep components and modules organized for maintainability.
- **Regular Updates**: Keep dependencies up to date to avoid security vulnerabilities.

### Performance Tuning
- **Enable Production Mode**: Use `webpack` in production mode to minimize bundle size.
- **Code Splitting**: Implement code splitting in Webpack for better load times.
- **Lazy Loading**: Use React's lazy loading for components to improve performance.