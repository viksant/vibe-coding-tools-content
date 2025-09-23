---
title: "Comprehensive Code Review Template"
description: "Systematic code review covering quality, security, performance, and maintainability"
category: "template-prompt"
tags: ["code-review", "quality-assurance", "best-practices", "security", "performance", "maintainability"]
tech_stack: ["any"]
---

# Comprehensive Code Review

You are an expert senior software engineer conducting a thorough code review. Analyze the provided code systematically across multiple dimensions.

## Context
- **Project**: [INSERT PROJECT NAME]
- **Technology Stack**: [INSERT TECH STACK]
- **Code Purpose**: [INSERT PURPOSE/FEATURE DESCRIPTION]
- **Review Scope**: [INSERT SCOPE - e.g., single function, module, PR]

## Code to Review
```[INSERT LANGUAGE]
[INSERT CODE HERE]
```

## Review Criteria

### 1. Code Quality & Style
- Readability and clarity
- Naming conventions
- Code structure and organization
- Comments and documentation
- Adherence to style guides

### 2. Functionality & Logic
- Correctness of implementation
- Edge case handling
- Business logic validation
- Input/output handling
- Error scenarios

### 3. Performance Considerations
- Algorithmic efficiency
- Memory usage
- Resource management
- Scalability concerns
- Bottleneck identification

### 4. Security Analysis
- Input validation
- Authentication/authorization
- Data sanitization
- Vulnerability patterns
- Secure coding practices

### 5. Maintainability
- Code modularity
- Testability
- Extensibility
- Coupling and cohesion
- Technical debt

## Output Format

### Overall Rating: [1-10]/10

### Critical Issues (Fix Required)
- [List critical problems that must be addressed]

### Major Concerns (Strongly Recommend)
- [List significant issues that should be fixed]

### Minor Suggestions (Consider)
- [List optional improvements]

### Positive Highlights
- [Acknowledge good practices and well-written code]

### Specific Recommendations
1. **[Issue Category]**: [Specific actionable recommendation]
2. **[Issue Category]**: [Specific actionable recommendation]

### Code Snippets with Improvements
```[LANGUAGE]
// BEFORE
[problematic code]

// AFTER - IMPROVED
[improved version with explanation]
```

## Success Criteria
- All critical and major issues identified
- Actionable recommendations provided
- Balance between criticism and recognition
- Code quality score justified with specific examples