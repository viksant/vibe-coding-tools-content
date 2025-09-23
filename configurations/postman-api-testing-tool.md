---
title: Postman API Testing Tool
description: >-
  Comprehensive API development platform for testing, documentation, and
  automation with collection management and mock servers
author: viksant
date: "2025-09-23"
tags:
  - api
  - testing
  - postman
  - automation
tech_stack:
  - JavaScript
  - REST API
  - HTTP
category: configurations
subcategory: general
tool: postman
---

# Postman API Testing Tool

## Comprehensive API Development Platform

### Key Features
- **API Testing**: Send HTTP requests and validate responses
- **Collection Management**: Organize related API calls
- **Environment Variables**: Manage different configurations
- **Automated Testing**: Pre-request and test scripts
- **Mock Servers**: Create mock endpoints for development
- **Documentation**: Generate interactive API documentation

### Request Types Supported
```yaml
methods:
  - GET: Retrieve data
  - POST: Create new resources
  - PUT: Update existing resources
  - PATCH: Partial updates
  - DELETE: Remove resources
  - HEAD: Get headers only
  - OPTIONS: Check allowed methods
```

### Advanced Features
```javascript
// Pre-request script example
pm.environment.set("timestamp", Date.now());
pm.environment.set("userId", pm.variables.get("randomUserId"));

// Test script example
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response time is less than 200ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(200);
});

pm.test("User ID is returned", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.user.id).to.exist;
});
```

### Collection Structure
- **Folders**: Organize requests by feature/module
- **Variables**: Collection-level and environment-level
- **Authorization**: Bearer tokens, API keys, OAuth
- **Pre-request Scripts**: Data setup and authentication
- **Tests**: Response validation and data extraction