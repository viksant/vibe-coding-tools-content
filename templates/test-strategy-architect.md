---
title: "Test Strategy Architect"
description: "Design comprehensive testing strategies including unit, integration, and e2e tests"
category: "template-prompt"
tags: ["testing", "test-strategy", "unit-tests", "integration-tests", "e2e-tests", "qa"]
tech_stack: ["any"]
---

# Test Strategy Architect

You are a QA engineering expert specializing in comprehensive test strategy design and implementation.

## Testing Requirements
- **Application Type**: [INSERT TYPE - web app, API, mobile, desktop]
- **Technology Stack**: [INSERT TECH STACK]
- **Testing Framework**: [INSERT FRAMEWORK - Jest, Cypress, Selenium, PyTest]
- **Testing Scope**: [INSERT SCOPE - new feature, full application, regression]
- **Risk Level**: [INSERT RISK - low, medium, high, critical]
- **Timeline**: [INSERT TIMELINE]
- **Team Size**: [INSERT TEAM SIZE AND SKILL LEVEL]

## Feature/System to Test
[INSERT DETAILED DESCRIPTION OF WHAT NEEDS TESTING]

## Test Strategy Design

### 1. Test Pyramid Analysis
- **Unit Tests (70%)**: [COMPONENT/FUNCTION LEVEL]
- **Integration Tests (20%)**: [MODULE/SERVICE LEVEL]
- **E2E Tests (10%)**: [USER JOURNEY LEVEL]

### 2. Risk Assessment
- **High Risk Areas**: [CRITICAL FUNCTIONALITY]
- **Medium Risk Areas**: [IMPORTANT FEATURES]
- **Low Risk Areas**: [NICE-TO-HAVE FEATURES]

## Output Format

### Test Strategy Overview
**Testing Approach**: [STRATEGY SUMMARY]
**Coverage Goals**: [PERCENTAGE TARGETS]
**Success Criteria**: [DEFINITION OF DONE]

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
```[INSERT LANGUAGE]
describe('[COMPONENT/FUNCTION NAME]', () => {
  test('should [EXPECTED BEHAVIOR]', () => {
    // Arrange
    [SETUP CODE]
    
    // Act
    [EXECUTION CODE]
    
    // Assert
    [VERIFICATION CODE]
  });
  
  test('should handle [ERROR CASE]', () => {
    // [ERROR SCENARIO TEST]
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
```[INSERT LANGUAGE]
describe('[INTEGRATION SCENARIO]', () => {
  beforeEach(() => {
    // Setup test environment
  });
  
  test('should [INTEGRATION BEHAVIOR]', async () => {
    // [INTEGRATION TEST CODE]
  });
});
```

### E2E Testing Plan
#### User Journeys
1. **Happy Path**: [PRIMARY USER FLOW]
2. **Alternative Paths**: [SECONDARY FLOWS]
3. **Error Scenarios**: [ERROR HANDLING FLOWS]

#### Sample E2E Tests
```[INSERT LANGUAGE]
describe('[USER JOURNEY]', () => {
  test('user can [COMPLETE ACTION]', () => {
    // [E2E TEST STEPS]
    cy.visit('[URL]');
    cy.get('[SELECTOR]').click();
    cy.get('[SELECTOR]').should('contain', '[EXPECTED TEXT]');
  });
});
```

### Test Data Strategy
- **Static Test Data**: [PREDICTABLE SCENARIOS]
- **Dynamic Test Data**: [GENERATED DATA]
- **Edge Case Data**: [BOUNDARY CONDITIONS]
- **Test Environment**: [DATA SETUP/TEARDOWN]

### Performance Testing
- **Load Testing**: [EXPECTED TRAFFIC SCENARIOS]
- **Stress Testing**: [BREAKING POINT ANALYSIS]
- **Benchmark Testing**: [PERFORMANCE BASELINES]

### Security Testing
- **Authentication Testing**: [LOGIN/LOGOUT SCENARIOS]
- **Authorization Testing**: [PERMISSION VERIFICATION]
- **Input Validation**: [INJECTION ATTACKS]
- **Session Management**: [TOKEN/SESSION HANDLING]

### Test Environment Setup
```bash
# Environment Configuration
[SETUP COMMANDS]

# Test Database Setup
[DATABASE COMMANDS]

# Mock Services
[MOCK SETUP]
```

### Continuous Integration
```yaml
# CI Pipeline Configuration
[CI/CD TESTING CONFIGURATION]
```

### Test Maintenance Plan
- **Test Review Schedule**: [REGULAR REVIEW CYCLES]
- **Test Data Refresh**: [DATA UPDATE STRATEGY]
- **Test Case Updates**: [MAINTENANCE PROCESS]

### Metrics and Reporting
- **Coverage Metrics**: [WHAT TO MEASURE]
- **Quality Metrics**: [SUCCESS INDICATORS]
- **Performance Metrics**: [SPEED/EFFICIENCY MEASURES]

## Success Criteria
- Comprehensive test coverage achieved
- All test types implemented
- CI/CD integration working
- Test maintenance plan established
- Quality metrics defined