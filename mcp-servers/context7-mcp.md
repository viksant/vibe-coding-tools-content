---
title: Context7 MCP
description: >-
  Library documentation MCP server for resolving library IDs and retrieving
  up-to-date documentation with code examples
author: holabuenastardes6854
date: "2025-09-23"
tags:
  - documentation
  - library-resolution
  - api-reference
  - code-examples
tech_stack:
  - TypeScript
  - MCP
  - Context7
category: mcp-servers
---

# Context7 MCP

## Library Documentation MCP Server

### Features
- **Library Resolution**: Find Context7-compatible library IDs
- **Documentation Retrieval**: Get up-to-date docs and examples
- **Code Samples**: Access real-world implementation patterns
- **API References**: Comprehensive API documentation
- **Version Support**: Access specific library versions

### Tools Available
```yaml
tools:
  - resolve_library_id
  - get_library_docs
  - search_examples
  - get_api_reference
```

### Usage Examples
```typescript
// Resolve library ID
const library = await context7.resolveLibraryId({
  libraryName: "react"
});

// Get documentation
const docs = await context7.getLibraryDocs({
  context7CompatibleLibraryID: "/facebook/react",
  topic: "hooks",
  tokens: 5000
});

// Search for specific examples
const examples = await context7.searchExamples({
  library: "/vercel/next.js",
  query: "api routes middleware"
});
```

### Library Coverage
- Popular frameworks (React, Next.js, Vue, Angular)
- Backend libraries (Express, Fastify, Nest.js)
- Database ORMs (Prisma, Mongoose, TypeORM)
- Testing frameworks (Jest, Cypress, Playwright)
- DevOps tools (Docker, Kubernetes, CI/CD)