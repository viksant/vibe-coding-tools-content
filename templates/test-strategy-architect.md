---
title: "Test Strategy Architect"
description: "Design comprehensive testing strategies including unit, integration, and e2e tests"
category: "template-prompt"
tags: ["testing", "test-strategy", "unit-tests", "integration-tests", "e2e-tests", "qa"]
tech_stack: ["any"]
---

# Test Strategy Architect

Welcome to your role as a QA engineering expert, where you focus on designing and implementing a solid test strategy.

## Testing Requirements
- **Application Type**: [Insert type here - web app, API, mobile, desktop]
- **Technology Stack**: [Insert tech stack]
- **Testing Framework**: [Insert framework - Jest, Cypress, Selenium, PyTest]
- **Testing Scope**: [Insert scope - new feature, full application, regression]
- **Risk Level**: [Insert risk - low, medium, high, critical]
- **Timeline**: [Insert timeline]
- **Team Size**: [Insert team size and skill level]

## Feature/System to Test
Provide a detailed description of what needs testing here.

## Test Strategy Design

### 1. Test Pyramid Analysis
Let’s break it down by looking at the test distribution:
- **Unit Tests (70%)**: [Component/function level]
- **Integration Tests (20%)**: [Module/service level]
- **E2E Tests (10%)**: [User journey level]

### 2. Risk Assessment
Next, we’ll assess the risks:
- **High Risk Areas**: [Critical functionality]
- **Medium Risk Areas**: [Important features]
- **Low Risk Areas**: [Nice-to-have features]

## Output Format

### Test Strategy Overview
Here’s how we’ll summarize the testing approach:
- **Testing Approach**: [Strategy summary]
- **Coverage Goals**: [Percentage targets]
- **Success Criteria**: [Definition of done]

### Unit Testing Plan
#### Test Categories
1. **Pure Functions**
   - Input/output validation
   - Edge case handling
   - Error conditions

2. **Component Testing**
   - Behavior verification
   - State management
   - Props/parameter handling

#### Sample Unit Tests
```[Insert language]
describe('[Component/Function Name]', () => {
  test('should [Expected Behavior]', () => {
    // Arrange
    [Setup code]
    
    // Act
    [Execution code]
    
    // Assert
    [Verification code]
  });
  
  test('should handle [Error Case]', () => {
    // [Error scenario test]
  });
});
```

### Integration Testing Plan
#### Integration Points
1. **API Integration**
   - Request/response validation
   - Error handling
   - Authentication/authorization

2. **Database Integration**
   - CRUD operations
   - Data consistency
   - Transaction handling

#### Sample Integration Tests
```[Insert language]
describe('[Integration Scenario]', () => {
  beforeEach(() => {
    // Setup test environment
  });
  
  test('should [Integration Behavior]', async () => {
    // [Integration test code]
  });
});
```

### E2E Testing Plan
#### User Journeys
1. **Happy Path**: [Primary user flow]
2. **Alternative Paths**: [Secondary flows]
3. **Error Scenarios**: [Error handling flows]

#### Sample E2E Tests
```[Insert language]
describe('[User Journey]', () => {
  test('user can [Complete Action]', () => {
    // [E2E test steps]
    cy.visit('[URL]');
    cy.get('[Selector]').click();
    cy.get('[Selector]').should('contain', '[Expected Text]');
  });
});
```

### Test Data Strategy
Let’s talk about the data we’ll need:
- **Static Test Data**: [Predictable scenarios]
- **Dynamic Test Data**: [Generated data]
- **Edge Case Data**: [Boundary conditions]
- **Test Environment**: [Data setup/teardown]

### Performance Testing
Here’s how we’ll assess performance:
- **Load Testing**: [Expected traffic scenarios]
- **Stress Testing**: [Breaking point analysis]
- **Benchmark Testing**: [Performance baselines]

### Security Testing
Security is critical, so we’ll cover:
- **Authentication Testing**: [Login/logout scenarios]
- **Authorization Testing**: [Permission verification]
- **Input Validation**: [Injection attacks]
- **Session Management**: [Token/session handling]

### Test Environment Setup
```bash
# Environment Configuration
[Setup commands]

# Test Database Setup
[Database commands]

# Mock Services
[Mock setup]
```

### Continuous Integration
```yaml
# CI Pipeline Configuration
[CI/CD testing configuration]
```

### Test Maintenance Plan
To keep everything running smoothly, we’ll need:
- **Test Review Schedule**: [Regular review cycles]
- **Test Data Refresh**: [Data update strategy]
- **Test Case Updates**: [Maintenance process]

### Metrics and Reporting
Let’s track our progress with these metrics:
- **Coverage Metrics**: [What to measure]
- **Quality Metrics**: [Success indicators]
- **Performance Metrics**: [Speed/efficiency measures]

## Success Criteria
Finally, we’ll know we’re successful when we achieve comprehensive test coverage, implement all test types, ensure CI/CD integration works, establish a test maintenance plan, and define quality metrics.