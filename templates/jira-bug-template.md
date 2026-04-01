# Jira Bug Template

## Basic Information
- **Issue Type:** Bug
- **Project:** [Project Key]
- **Summary:** [Short description of the bug]
- **Priority:** [P0 (Critical) / P1 (High) / P2 (Medium) / P3 (Low)]
- **Severity:** [Blocker / Critical / Major / Minor]
- **Labels:** [bug], [affected-feature], [environment]
- **Affected Version(s):** [v1.2.3]

## Description

### Bug Summary
[Clear, concise description of the bug in 1-2 sentences]

### Impact
- **Users Affected:** [All users / Specific segment / % of users]
- **Business Impact:** [Revenue loss / User experience / Operations blocked]
- **Frequency:** [Always / Sometimes / Rarely]

---

## Steps to Reproduce

1. [Step 1: Navigate to...]
2. [Step 2: Click on...]
3. [Step 3: Enter data...]
4. [Step 4: Submit form...]
5. [Bug occurs at this step]

---

## Expected Behavior
[What should happen when following the steps above?]

---

## Actual Behavior
[What actually happens? What goes wrong?]

---

## Environment

### Device/Browser
- **Device:** [Desktop / Mobile / Tablet]
- **OS:** [Windows 11 / macOS 14.0 / iOS 17 / Android 13]
- **Browser:** [Chrome 120 / Safari 17 / Firefox 121]
- **Screen Resolution:** [1920x1080]

### Environment
- **Environment:** [Production / Staging / Development]
- **URL:** [https://example.com/page]
- **Backend Version:** [v2.5.0]
- **Frontend Version:** [v3.1.2]

### User Context
- **User ID:** [12345]
- **Account Type:** [Free / Premium / Enterprise]
- **Permissions:** [Admin / User / Guest]

---

## Screenshots / Videos
[Attach screenshots or screen recordings showing the bug]

---

## Logs / Error Messages

### Console Errors
```
[Paste browser console errors here]
```

### Backend Logs
```
[Paste relevant backend logs, stack traces]
```

### Network Requests
```
[Paste failed API requests, response codes]
```

---

## Root Cause (to be filled by Engineering)
[Analysis of what's causing the bug]

---

## Fix Approach (to be filled by Engineering)
[Proposed solution or fix strategy]

---

## Acceptance Criteria for Fix

- [ ] Bug no longer occurs when following reproduction steps
- [ ] No regression in related features
- [ ] Unit tests added to prevent regression
- [ ] Fix verified on all affected environments (dev, staging, prod)
- [ ] Fix verified on all affected devices/browsers

---

## Workaround (if available)
[Temporary workaround users can use while waiting for fix]

---

## Related Issues
- Related to: [ISSUE-XXX]
- Blocked by: [ISSUE-YYY]
- Blocks: [ISSUE-ZZZ]

---

## Priority Justification

**Why P0/P1/P2/P3?**
[Explain why this bug has this priority level]

---

## Definition of Done (Bug Fix)
- [ ] Root cause identified
- [ ] Fix implemented and code reviewed
- [ ] Unit tests added (if applicable)
- [ ] QA verified fix on staging
- [ ] No regression detected
- [ ] Deployed to production
- [ ] Verified in production
- [ ] Postmortem written (for P0/P1 bugs)

---

## Discovered By
- **Reporter:** [Name / Team]
- **Date Discovered:** [YYYY-MM-DD]
- **How Discovered:** [User report / Internal testing / Monitoring alert]

---

## Comments / Notes
[Any additional context, discussions, or findings]
