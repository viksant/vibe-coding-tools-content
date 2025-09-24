---
title: "Claude Code Next.js Fullstack"
description: "Optimizes Claude Code for Next.js fullstack development with App Router, Server Components, and API Routes."
category: "configuration"
tags: ["claude-code", "nextjs", "fullstack", "app-router", "server-components", "api-routes", "vercel", "prisma", "typescript"]
tech_stack: ["nextjs", "react", "typescript", "vercel", "prisma"]
---

This configuration optimizes Claude Code for Next.js fullstack development with App Router, Server Components, and API Routes.

### Configuration Overview
This setup provides a comprehensive development environment for building fullstack applications using Next.js 14+, featuring App Router, Server Components, optimized API Routes, and seamless Vercel deployment.

### Prerequisites
- Node.js (version 14.x or later)
- npm or Yarn (latest version)
- Vercel account for deployment
- Prisma CLI (version 3.x or later)

### Installation & Setup
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
   - Update the `DATABASE_URL` in `.env` with your database connection string.
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
6. **Create API routes** in the `pages/api` directory for handling requests.
7. **Deploy to Vercel**:
   ```bash
   npm install -g vercel
   vercel
   ```

### File Structure
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
- **Enable SWC for faster builds**:
  Add the following to `next.config.js`:
  ```javascript
  module.exports = {
    swcMinify: true,
  };
  ```
- **Optimize images** using Next.js Image component:
  ```typescript
  import Image from 'next/image';
  <Image src="/path/to/image.jpg" alt="Description" width={500} height={500} />
  ```

### Troubleshooting
- **Error: "PrismaClientInitializationError"**:
  Ensure your `DATABASE_URL` in `.env` is correct and the database is accessible.
- **Deployment issues on Vercel**:
  Check the Vercel logs for errors and ensure your environment variables are set correctly in the Vercel dashboard.

### Best Practices
- **Use TypeScript for type safety** throughout your application.
- **Keep API routes lean** by offloading heavy logic to services or utilities.
- **Implement error handling** in API routes to manage exceptions gracefully.

### Performance Tuning
- **Leverage Next.js caching** by using `getStaticProps` and `getServerSideProps` where appropriate.
- **Minimize bundle size** by using dynamic imports for large components:
  ```typescript
  const DynamicComponent = dynamic(() => import('./DynamicComponent'));
  ```
- **Monitor performance** using Vercel Analytics to identify bottlenecks and optimize accordingly.