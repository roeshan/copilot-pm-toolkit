# Jira User Story Template

## Basic Information
- **Issue Type:** Story
- **Project:** [Project Key]
- **Summary:** As a [persona], I want [capability], so that [value]
- **Priority:** [P0 / P1 / P2 / P3]
- **Labels:** [feature-name], [team-name], [sprint-name]

## Description

### User Story
As a **[persona]** (e.g., Product Manager, Customer, Merchant),  
I want **[capability/feature]**,  
So that **[business value/user benefit]**.

### Background / Context
[Why is this story needed? What problem does it solve?]

### Value Proposition
[What value does this provide to users/business?]

---

## Acceptance Criteria

### Scenario 1: [Happy Path]
**Given** [initial context/state],  
**When** [action is performed],  
**Then** [expected outcome].

### Scenario 2: [Edge Case]
**Given** [initial context/state],  
**When** [action is performed],  
**Then** [expected outcome].

### Scenario 3: [Error Handling]
**Given** [error condition],  
**When** [action is performed],  
**Then** [error message shown / fallback behavior].

---

## Technical Details

### API Contract (if applicable)
```
Endpoint: [POST/GET/PUT/DELETE] /api/v1/[resource]
Request: { ... }
Response: { ... }
```

### Data Model Changes
[Any database schema changes, new fields, migrations needed]

### Dependencies
- [ ] Dependency 1: [Description, Owner, Status]
- [ ] Dependency 2: [Description, Owner, Status]

---

## Design / Mockups
[Link to Figma or attach screenshots]

---

## Testing Requirements

### Unit Tests
- [ ] Test scenario 1
- [ ] Test scenario 2

### Integration Tests
- [ ] Test API endpoint
- [ ] Test data flow

### Manual QA
- [ ] Test on devices: [iOS, Android, Web]
- [ ] Test edge cases

---

## Definition of Done
- [ ] Code complete and merged to main
- [ ] Unit tests written and passing (>80% coverage)
- [ ] Integration tests passing
- [ ] Code reviewed by 2+ engineers
- [ ] QA tested on staging
- [ ] Documentation updated (README, API docs)
- [ ] Deployed to production
- [ ] Metrics/tracking implemented (Analytics events)

---

## Story Points
[Estimate: 1, 2, 3, 5, 8, 13, 21]

---

## Sprint
[Sprint name or sprint ID]

---

## Epic Link
[EPIC-XXX]: [Epic Name]

---

## Comments / Notes
[Any additional context, discussions, decisions made]
