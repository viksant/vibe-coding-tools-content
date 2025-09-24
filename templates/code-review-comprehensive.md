---
title: "Comprehensive Code Review Template"
description: "Systematic code review covering quality, security, performance, and maintainability"
category: "template-prompt"
tags: ["code-review", "quality-assurance", "best-practices", "security", "performance", "maintainability"]
tech_stack: ["any"]
---

# Comprehensive Code Review

As a seasoned software engineer, you're stepping into the role of reviewer. Your task is to analyze the provided code thoroughly and from various angles.

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
Let's start with the basics. Check for:
- Readability and clarity
- Consistent naming conventions
- Logical structure and organization
- Adequate comments and documentation
- Compliance with style guides

### 2. Functionality & Logic
Next up, dive into the functionality. Look for:
- Correct implementation
- Handling of edge cases
- Validation of business logic
- Proper input/output management
- Consideration of error scenarios

### 3. Performance Considerations
Performance matters too. Focus on:
- Efficiency of algorithms
- Memory usage
- Resource management
- Scalability issues
- Identification of bottlenecks

### 4. Security Analysis
Security is critical. Evaluate:
- Input validation processes
- Authentication and authorization measures
- Data sanitization efforts
- Patterns that indicate vulnerabilities
- Adherence to secure coding practices

### 5. Maintainability
Finally, assess maintainability. Examine:
- Modularity of the code
- Ease of testing
- Potential for extensibility
- Coupling and cohesion levels
- Any existing technical debt

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
To wrap it up, ensure you meet these goals:
- Identify all critical and major issues
- Provide actionable recommendations
- Balance your feedback between critique and praise
- Justify the code quality score with specific examples