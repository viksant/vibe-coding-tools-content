---
title: Express API Starter Template
description: >-
  Production-ready REST API template with Express.js, TypeScript, PostgreSQL,
  and JWT authentication
author: holabuenastardes6854
date: "2025-09-23"
tags:
  - express
  - api
  - typescript
  - postgresql
tech_stack:
  - Express.js
  - TypeScript
  - PostgreSQL
category: template-prompts
use_case: code review
---

# Express API Starter Template

## Production-Ready REST API Template

### Features
- **Express.js** with TypeScript
- **PostgreSQL** with Prisma ORM
- **JWT Authentication**
- **Input validation** with Joi
- **API documentation** with Swagger
- **Rate limiting** and security middleware

### Project Structure
```
├── src/
│   ├── controllers/
│   ├── middleware/
│   ├── models/
│   ├── routes/
│   ├── services/
│   ├── utils/
│   └── app.ts
├── prisma/
│   ├── schema.prisma
│   └── migrations/
├── tests/
└── docs/
```

### Example Controller
```typescript
import { Request, Response } from 'express';
import { UserService } from '../services/user.service';

export class UserController {
  static async getUsers(req: Request, res: Response) {
    try {
      const users = await UserService.getAllUsers();
      res.json({ success: true, data: users });
    } catch (error) {
      res.status(500).json({
        success: false,
        error: error.message
      });
    }
  }
}
```

### Security Features
- Helmet for security headers
- CORS configuration
- Rate limiting
- Input sanitization
- SQL injection prevention

### Deployment Ready
- Docker configuration
- Environment management
- Health checks
- Logging with Winston