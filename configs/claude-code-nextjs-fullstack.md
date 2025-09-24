---
title: "Claude Code Next.js Fullstack"
description: "Optimizes Claude Code for Next.js fullstack development with App Router, Server Components, and API Routes."
category: "configuration"
tags: ["claude-code", "nextjs", "fullstack", "app-router", "server-components", "api-routes", "vercel", "prisma", "typescript"]
tech_stack: ["nextjs", "react", "typescript", "vercel", "prisma"]
---

This configuration sets you up to work with Claude Code for fullstack development using Next.js, complete with App Router, Server Components, and API Routes.

### Configuration Overview
This setup creates a solid development environment for building fullstack applications with Next.js 14 or later. It features an App Router, Server Components, optimized API Routes, and smooth deployment to Vercel.

### Prerequisites
Before you dive in, make sure you have:
- Node.js (version 14.x or later)
- npm or Yarn (latest version)
- A Vercel account for deployment
- Prisma CLI (version 3.x or later)

### Installation & Setup
Let's get started with the installation process:

1. **Initialize a new Next.js project**:
   ```bash
   npx create-next-app@latest my-next-app --typescript
   cd my-next-app
   ```
2. **Install required dependencies**:
   ```bash
   npm install prisma @prisma/client
   ```
3. **Set up Prisma**:
   ```bash
   npx prisma init
   ```
   You’ll want to update the `DATABASE_URL` in your `.env` file with your database connection string.
4. **Define your data model in `schema.prisma`**:
   ```prisma
   datasource db {
     provider = "postgresql"
     url      = env("DATABASE_URL")
   }
   generator client {
     provider = "prisma-client-js"
   }
   model User {
     id    Int     @id @default(autoincrement())
     name  String
     email String  @unique
   }
   ```
5. **Run Prisma migrations**:
   ```bash
   npx prisma migrate dev --name init
   ```
6. **Create API routes** in the `pages/api` directory to handle your requests.
7. **Deploy to Vercel**:
   ```bash
   npm install -g vercel
   vercel
   ```

### File Structure
Here’s how your project structure should look:
```
my-next-app/
├── node_modules/
├── pages/
│   ├── api/
│   │   └── users.ts
│   ├── _app.tsx
│   └── index.tsx
├── prisma/
│   └── schema.prisma
├── public/
├── styles/
│   └── globals.css
├── .env
├── package.json
└── tsconfig.json
```

### Key Configuration Files
- **`schema.prisma`**:
  ```prisma
  datasource db {
    provider = "postgresql"
    url      = env("DATABASE_URL")
  }
  generator client {
    provider = "prisma-client-js"
  }
  model User {
    id    Int     @id @default(autoincrement())
    name  String
    email String  @unique
  }
  ```
- **`pages/api/users.ts`**:
  ```typescript
  import { NextApiRequest, NextApiResponse } from 'next';
  import { PrismaClient } from '@prisma/client';

  const prisma = new PrismaClient();

  export default async function handler(req: NextApiRequest, res: NextApiResponse) {
    if (req.method === 'GET') {
      const users = await prisma.user.findMany();
      res.json(users);
    } else if (req.method === 'POST') {
      const { name, email } = req.body;
      const user = await prisma.user.create({ data: { name, email } });
      res.json(user);
    }
  }
  ```

### Advanced Options
Let’s take things up a notch:

- **Enable SWC for faster builds**:
  Add this to your `next.config.js`:
  ```javascript
  module.exports = {
    swcMinify: true,
  };
  ```
- **Optimize images** using the Next.js Image component:
  ```typescript
  import Image from 'next/image';
  <Image src="/path/to/image.jpg" alt="Description" width={500} height={500} />
  ```

### Troubleshooting
If you run into issues, here are a few tips:

- **Error: "PrismaClientInitializationError"**:
  Double-check the `DATABASE_URL` in your `.env` file and ensure the database is reachable.
- **Deployment issues on Vercel**:
  Look at the Vercel logs for any errors and make sure your environment variables are correctly set in the Vercel dashboard.

### Best Practices
Keep these tips in mind as you work:

- **Use TypeScript for type safety** throughout your application.
- **Keep API routes lean** by moving heavy logic into separate services or utilities.
- **Implement error handling** in your API routes to manage exceptions effectively.

### Performance Tuning
Here are some ways to boost performance:

- **Leverage Next.js caching** with `getStaticProps` and `getServerSideProps` when it makes sense.
- **Minimize bundle size** by using dynamic imports for large components:
  ```typescript
  const DynamicComponent = dynamic(() => import('./DynamicComponent'));
  ```
- **Monitor performance** using Vercel Analytics to spot bottlenecks and improve your application.