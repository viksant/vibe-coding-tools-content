---
title: API Design Rules
description: >-
  RESTful API development standards and best practices for consistent, secure,
  and maintainable backend services
author: holabuenastardes6854
date: "2025-09-23"
tags:
  - api
  - rest
  - backend
  - validation
tech_stack:
  - TypeScript
  - Next.js
  - Zod
category: rules
---

# API Design Rules

## RESTful API Development Standards

### URL Structure
```yaml
# ✅ Good: RESTful URL patterns
GET    /api/users              # List users
GET    /api/users/123          # Get specific user
POST   /api/users              # Create user
PUT    /api/users/123          # Update user (full)
PATCH  /api/users/123          # Update user (partial)
DELETE /api/users/123          # Delete user

# ✅ Good: Nested resources
GET    /api/users/123/posts    # Get user's posts
POST   /api/users/123/posts    # Create post for user

# ❌ Avoid: Non-RESTful patterns
GET    /api/getUserById/123    # Too verbose
POST   /api/deleteUser         # Wrong method
GET    /api/users?delete=123   # Action in query
```

### Response Format Standards
```typescript
// ✅ Good: Consistent response structure
interface ApiResponse<T> {
  success: boolean;
  data?: T;
  error?: string;
  message?: string;
  pagination?: {
    page: number;
    limit: number;
    total: number;
    hasNext: boolean;
  };
}

// ✅ Good: Success response
{
  "success": true,
  "data": {
    "id": "123",
    "name": "John Doe",
    "email": "john@example.com"
  }
}

// ✅ Good: Error response
{
  "success": false,
  "error": "VALIDATION_ERROR",
  "message": "Email is required",
  "details": {
    "field": "email",
    "code": "REQUIRED"
  }
}
```

### HTTP Status Codes
```yaml
# Success responses
200: OK                 # Successful GET, PUT, PATCH
201: Created           # Successful POST
204: No Content        # Successful DELETE

# Client errors
400: Bad Request       # Invalid request data
401: Unauthorized      # Authentication required
403: Forbidden         # Insufficient permissions
404: Not Found         # Resource doesn't exist
409: Conflict          # Resource already exists
422: Unprocessable     # Validation errors

# Server errors
500: Internal Error    # Server-side error
502: Bad Gateway       # Upstream service error
503: Service Unavailable # Temporary unavailable
```

### Input Validation
```typescript
// ✅ Good: Comprehensive validation
import { z } from 'zod';

const CreateUserSchema = z.object({
  name: z.string().min(1).max(100),
  email: z.string().email(),
  age: z.number().int().min(13).max(120),
  role: z.enum(['user', 'admin', 'moderator'])
});

export async function POST(request: Request) {
  try {
    const body = await request.json();
    const validatedData = CreateUserSchema.parse(body);

    const user = await createUser(validatedData);
    return Response.json({
      success: true,
      data: user
    }, { status: 201 });

  } catch (error) {
    if (error instanceof z.ZodError) {
      return Response.json({
        success: false,
        error: 'VALIDATION_ERROR',
        message: 'Invalid input data',
        details: error.errors
      }, { status: 422 });
    }

    return Response.json({
      success: false,
      error: 'INTERNAL_ERROR',
      message: 'Something went wrong'
    }, { status: 500 });
  }
}
```

### Security Rules
```typescript
// ✅ Good: Security headers and validation
export async function middleware(request: NextRequest) {
  const response = NextResponse.next();

  // Security headers
  response.headers.set('X-Content-Type-Options', 'nosniff');
  response.headers.set('X-Frame-Options', 'DENY');
  response.headers.set('X-XSS-Protection', '1; mode=block');

  // Rate limiting (implement with Redis or similar)
  const ip = request.ip || 'unknown';
  const isRateLimited = await checkRateLimit(ip);

  if (isRateLimited) {
    return Response.json({
      success: false,
      error: 'RATE_LIMITED',
      message: 'Too many requests'
    }, { status: 429 });
  }

  return response;
}

// ✅ Good: Input sanitization
function sanitizeInput(input: string): string {
  return input
    .trim()
    .replace(/[<>]/g, '') // Remove potential XSS characters
    .substring(0, 1000);   // Limit length
}
```