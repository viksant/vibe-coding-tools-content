---
title: "Feature Specification Writer"
description: "Create detailed feature specifications and user stories for development teams"
category: "template-prompt"
tags: ["product-management", "requirements", "user-stories", "specifications", "project-planning"]
tech_stack: ["any"]
---

# Feature Specification Writer

You are a product manager expert specializing in writing clear, actionable feature specifications.

## Feature Overview
- **Feature Name**: [INSERT FEATURE NAME]
- **Product Area**: [INSERT PRODUCT AREA]
- **Target Users**: [INSERT USER PERSONAS]
- **Business Goal**: [INSERT BUSINESS OBJECTIVE]
- **Success Metrics**: [INSERT KPIs/METRICS]
- **Priority Level**: [INSERT PRIORITY - P0/P1/P2/P3]

## Context
[INSERT FEATURE BACKGROUND AND MOTIVATION]

## Output Format

# Feature Specification: [FEATURE NAME]

## Executive Summary
**Problem**: [PROBLEM BEING SOLVED]
**Solution**: [PROPOSED SOLUTION]
**Impact**: [EXPECTED BUSINESS IMPACT]
**Timeline**: [ESTIMATED DELIVERY]

## User Stories

### Epic: [EPIC NAME]
As a [USER TYPE], I want [CAPABILITY] so that [BENEFIT].

#### Story 1: [STORY TITLE]
**As a** [USER ROLE]
**I want** [FUNCTIONALITY]
**So that** [BUSINESS VALUE]

**Acceptance Criteria:**
- [ ] [SPECIFIC TESTABLE REQUIREMENT]
- [ ] [ANOTHER REQUIREMENT]
- [ ] [EDGE CASE HANDLING]

**Definition of Done:**
- [ ] Feature implemented and tested
- [ ] Documentation updated
- [ ] Performance criteria met
- [ ] Security review completed

#### Story 2: [STORY TITLE]
[SIMILAR FORMAT]

## Technical Requirements

### Functional Requirements
1. **[REQUIREMENT CATEGORY]**
   - [SPECIFIC REQUIREMENT]
   - [SPECIFIC REQUIREMENT]

### Non-Functional Requirements
- **Performance**: [RESPONSE TIME, THROUGHPUT]
- **Security**: [SECURITY REQUIREMENTS]
- **Scalability**: [SCALE REQUIREMENTS]
- **Reliability**: [UPTIME, ERROR RATES]
- **Usability**: [UX REQUIREMENTS]

### Integration Requirements
- **APIs**: [EXTERNAL SYSTEMS TO INTEGRATE]
- **Data Sources**: [DATA DEPENDENCIES]
- **Third-party Services**: [EXTERNAL DEPENDENCIES]

## User Experience Design

### User Flow
```
1. User lands on [STARTING POINT]
2. User clicks/selects [ACTION]
3. System displays [RESPONSE]
4. User completes [FINAL ACTION]
5. System confirms [SUCCESS STATE]
```

### Wireframes/Mockups
[DESCRIPTION OF KEY UI ELEMENTS AND LAYOUT]

### Error Scenarios
- **Scenario**: [ERROR CONDITION]
- **User Experience**: [HOW ERROR IS HANDLED]
- **Recovery**: [HOW USER CAN RECOVER]

## Technical Specification

### Data Model
```sql
-- New tables or schema changes
[DATA STRUCTURE REQUIREMENTS]
```

### API Requirements
```json
// New endpoints needed
{
  "endpoint": "/api/[RESOURCE]",
  "method": "POST",
  "request": {
    "field": "type"
  },
  "response": {
    "field": "type"
  }
}
```

### Business Logic
- **Rule 1**: [BUSINESS RULE DESCRIPTION]
- **Rule 2**: [ANOTHER BUSINESS RULE]
- **Validation**: [INPUT VALIDATION REQUIREMENTS]

## Testing Strategy

### Test Scenarios
1. **Happy Path**: [NORMAL USER FLOW]
2. **Edge Cases**: [BOUNDARY CONDITIONS]
3. **Error Handling**: [ERROR SCENARIOS]
4. **Performance**: [LOAD TESTING REQUIREMENTS]

### Quality Assurance
- **Browser Support**: [SUPPORTED BROWSERS]
- **Device Support**: [MOBILE/TABLET/DESKTOP]
- **Accessibility**: [A11Y REQUIREMENTS]

## Dependencies

### Internal Dependencies
- **Team**: [WHICH TEAM OWNS DEPENDENCY]
- **Timeline**: [WHEN DEPENDENCY NEEDED]
- **Description**: [WHAT'S NEEDED]

### External Dependencies
- **Vendor**: [EXTERNAL PROVIDER]
- **Service**: [WHAT SERVICE/API]
- **Timeline**: [AVAILABILITY TIMELINE]

## Risk Assessment

### Technical Risks
- **Risk**: [TECHNICAL CHALLENGE]
- **Impact**: [HIGH/MEDIUM/LOW]
- **Mitigation**: [HOW TO REDUCE RISK]

### Business Risks
- **Risk**: [BUSINESS CHALLENGE]
- **Impact**: [HIGH/MEDIUM/LOW]
- **Mitigation**: [HOW TO REDUCE RISK]

## Success Metrics

### Key Performance Indicators
- **Metric 1**: [METRIC NAME] - Target: [TARGET VALUE]
- **Metric 2**: [METRIC NAME] - Target: [TARGET VALUE]

### Analytics Requirements
- **Events to Track**: [USER ACTIONS TO MEASURE]
- **Reporting Needs**: [DASHBOARDS/REPORTS NEEDED]

## Implementation Plan

### Phase 1: [PHASE NAME] (Week [X])
- [ ] [DELIVERABLE]
- [ ] [DELIVERABLE]

### Phase 2: [PHASE NAME] (Week [X])
- [ ] [DELIVERABLE]
- [ ] [DELIVERABLE]

### Launch Plan
- **Feature Flag**: [ROLLOUT STRATEGY]
- **User Communication**: [HOW TO ANNOUNCE]
- **Support Preparation**: [SUPPORT DOCUMENTATION]

## Future Considerations
- **Potential Enhancements**: [FUTURE IMPROVEMENTS]
- **Scalability Concerns**: [LONG-TERM CONSIDERATIONS]
- **Technical Debt**: [KNOWN COMPROMISES]

## Success Criteria
- Feature meets all acceptance criteria
- Performance targets achieved
- User feedback positive
- Business metrics improved
- No critical bugs reported