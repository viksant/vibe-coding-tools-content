---
title: "API Endpoint Generator"
description: "Generate complete REST API endpoints with validation, error handling, and documentation"
category: "template-prompt"
tags: ["api-design", "rest", "backend", "validation", "documentation", "error-handling"]
tech_stack: ["express", "fastapi", "django", "spring-boot", "any"]
---

# API Endpoint Generator

You are an expert backend developer specializing in RESTful API design. Create a complete, production-ready API endpoint.

## Requirements
- **Framework**: [INSERT FRAMEWORK - e.g., Express.js, FastAPI, Django REST]
- **Endpoint Purpose**: [INSERT PURPOSE - e.g., user registration, product search]
- **HTTP Method**: [INSERT METHOD - GET/POST/PUT/DELETE]
- **Route**: [INSERT ROUTE - e.g., /api/v1/users]
- **Authentication**: [INSERT AUTH TYPE - JWT, OAuth, API Key, None]
- **Database**: [INSERT DATABASE - PostgreSQL, MongoDB, etc.]

## Data Structure
### Request Schema
```json
[INSERT REQUEST BODY SCHEMA OR "N/A for GET"]
```

### Response Schema
```json
[INSERT EXPECTED RESPONSE SCHEMA]
```

## Business Logic
[INSERT SPECIFIC BUSINESS RULES AND VALIDATION REQUIREMENTS]

## Generate Complete Endpoint

Include the following components:

### 1. Route Handler
- Complete endpoint implementation
- Request validation
- Business logic processing
- Response formatting

### 2. Input Validation
- Schema validation
- Type checking
- Required field validation
- Custom business rule validation

### 3. Error Handling
- Validation errors (400)
- Authentication errors (401)
- Authorization errors (403)
- Not found errors (404)
- Server errors (500)

### 4. Security Measures
- Input sanitization
- Rate limiting consideration
- Authentication/authorization
- SQL injection prevention

### 5. Response Formatting
- Success responses
- Error responses
- Consistent structure
- Appropriate HTTP status codes

### 6. Documentation
- OpenAPI/Swagger documentation
- Usage examples
- Parameter descriptions

### 7. Tests
- Unit tests for business logic
- Integration tests for full endpoint
- Edge case testing
- Error scenario testing

## Output Format

```[INSERT LANGUAGE]
// [ENDPOINT IMPLEMENTATION]
```

### Documentation
```yaml
# OpenAPI Specification
[SWAGGER/OPENAPI DOCS]
```

### Tests
```[INSERT LANGUAGE]
// [TEST IMPLEMENTATION]
```

## Success Criteria
- Endpoint handles all specified requirements
- Comprehensive error handling
- Security best practices implemented
- Full test coverage
- Clear documentation provided