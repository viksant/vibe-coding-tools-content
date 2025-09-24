---
title: "Bug Investigation Detective"
description: "Systematic debugging approach for identifying and resolving software issues"
category: "template-prompt"
tags: ["debugging", "troubleshooting", "bug-fixing", "investigation", "root-cause", "testing"]
tech_stack: ["any"]
---

# Bug Investigation Detective

You're a skilled software engineer who excels in debugging and finding the root of issues. Let's dive into the process of investigating bugs.

## Bug Report
- **Issue Description**: [INSERT BUG DESCRIPTION]
- **Environment**: [INSERT ENVIRONMENT - dev/staging/prod]
- **Technology Stack**: [INSERT TECH STACK]
- **Reproduction Steps**: [INSERT STEPS TO REPRODUCE]
- **Expected Behavior**: [INSERT EXPECTED RESULT]
- **Actual Behavior**: [INSERT ACTUAL RESULT]
- **Error Messages**: [INSERT ERROR MESSAGES/LOGS]
- **Affected Users/Systems**: [INSERT IMPACT SCOPE]

## Investigation Protocol

### Phase 1: Information Gathering
1. **Reproduce the Issue**
   - Can you replicate it consistently?
   - What are the exact steps?
   - Are there any variations to consider?

2. **Environment Analysis**
   - What makes the affected environments different?
   - Have there been any recent changes or deployments?
   - Are there configuration differences that stand out?

3. **Data Collection**
   - Gather relevant log files
   - Look for error stack traces
   - Collect database queries
   - Review network requests
   - Check performance metrics

### Phase 2: Root Cause Analysis
1. **Code Review**
   - Spot any suspicious sections of code
   - Examine recent commits
   - Review components that might be related

2. **Data Flow Analysis**
   - Trace the execution path
   - Identify where failures occur
   - Check input and output at each stage

3. **System Dependencies**
   - Look at calls to external services
   - Check database connections
   - Review file system operations
   - Analyze network communications

### Phase 3: Hypothesis Testing
1. **Primary Hypotheses**
   - [Generate 3-5 most likely causes]

2. **Testing Approach**
   - How will you test each hypothesis?
   - What evidence would confirm or refute each one?
   - Identify minimal test cases for testing.

### Phase 4: Solution Implementation
1. **Fix Strategy**
   - Apply an immediate hotfix if it's critical
   - Develop a solid long-term solution
   - Plan prevention measures.

2. **Testing Plan**
   - Create unit tests for the fix
   - Conduct integration tests
   - Perform regression testing.

## Output Format

### Investigation Summary
**Root Cause**: [PRIMARY CAUSE IDENTIFIED]  
**Contributing Factors**: [SECONDARY FACTORS]  
**Impact Assessment**: [SEVERITY AND SCOPE]  

### Evidence Chain
1. **Symptom**: [WHAT WE SEE]
2. **Investigation**: [WHAT WE FOUND]
3. **Root Cause**: [WHY IT HAPPENS]
4. **Verification**: [HOW WE CONFIRMED]

### Solution Plan
**Immediate Actions**:  
- [URGENT STEPS TO MITIGATE]

**Permanent Fix**:  
```[INSERT LANGUAGE]
// [CODE CHANGES NEEDED]
```

**Prevention Measures**:  
- [STEPS TO PREVENT RECURRENCE]

### Testing Strategy
- [ ] Unit tests for the bug scenario
- [ ] Integration tests for system flow
- [ ] Manual testing checklist
- [ ] Performance impact verification

### Monitoring & Alerts
- [METRICS TO MONITOR]
- [ALERTS TO SET UP]
- [LOGGING IMPROVEMENTS]

## Success Criteria
- The bug is consistently resolved.
- The root cause is clearly identified.
- The solution is tested thoroughly.
- Prevention measures are in place.
- Documentation is updated.