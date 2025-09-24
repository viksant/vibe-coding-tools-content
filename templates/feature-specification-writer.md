---
title: "Feature Specification Writer"
description: "Create detailed feature specifications and user stories for development teams"
category: "template-prompt"
tags: ["product-management", "requirements", "user-stories", "specifications", "project-planning"]
tech_stack: ["any"]
---

# Feature Specification: [FEATURE NAME]

## Executive Summary
**Problem**: [What issue are we addressing?]  
**Solution**: [What’s the proposed fix?]  
**Impact**: [What business benefit do we expect?]  
**Timeline**: [When do we plan to deliver this?]  

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
[Continue in a similar format]

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
[Describe the key UI elements and layout]

### Error Scenarios
- **Scenario**: [Describe the error condition]  
- **User Experience**: [Explain how the error is handled]  
- **Recovery**: [Outline how the user can recover]  

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
- **Rule 1**: [Describe the business rule]  
- **Rule 2**: [Another business rule]  
- **Validation**: [Input validation requirements]  

## Testing Strategy

### Test Scenarios
1. **Happy Path**: [Describe the normal user flow]  
2. **Edge Cases**: [Outline boundary conditions]  
3. **Error Handling**: [Describe error scenarios]  
4. **Performance**: [Specify load testing requirements]  

### Quality Assurance
- **Browser Support**: [List supported browsers]  
- **Device Support**: [Specify mobile/tablet/desktop]  
- **Accessibility**: [Outline accessibility requirements]  

## Dependencies

### Internal Dependencies
- **Team**: [Which team owns this dependency?]  
- **Timeline**: [When do we need it?]  
- **Description**: [What’s required?]  

### External Dependencies
- **Vendor**: [Which external provider?]  
- **Service**: [What service or API?]  
- **Timeline**: [When will it be available?]  

## Risk Assessment

### Technical Risks
- **Risk**: [Describe the technical challenge]  
- **Impact**: [Assess the impact: high/medium/low]  
- **Mitigation**: [Explain how to reduce this risk]  

### Business Risks
- **Risk**: [Describe the business challenge]  
- **Impact**: [Assess the impact: high/medium/low]  
- **Mitigation**: [Explain how to reduce this risk]  

## Success Metrics

### Key Performance Indicators
- **Metric 1**: [METRIC NAME] - Target: [TARGET VALUE]  
- **Metric 2**: [METRIC NAME] - Target: [TARGET VALUE]  

### Analytics Requirements
- **Events to Track**: [User actions to measure]  
- **Reporting Needs**: [Dashboards/reports needed]  

## Implementation Plan

### Phase 1: [PHASE NAME] (Week [X])
- [ ] [DELIVERABLE]  
- [ ] [DELIVERABLE]  

### Phase 2: [PHASE NAME] (Week [X])
- [ ] [DELIVERABLE]  
- [ ] [DELIVERABLE]  

### Launch Plan
- **Feature Flag**: [Rollout strategy]  
- **User Communication**: [How will we announce it?]  
- **Support Preparation**: [What support documentation is needed?]  

## Future Considerations
- **Potential Enhancements**: [Future improvements]  
- **Scalability Concerns**: [Long-term considerations]  
- **Technical Debt**: [Known compromises]  

## Success Criteria
- Feature meets all acceptance criteria  
- Performance targets achieved  
- User feedback positive  
- Business metrics improved  
- No critical bugs reported