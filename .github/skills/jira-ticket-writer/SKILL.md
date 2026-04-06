---
name: jira-ticket-writer
description: "Use when: creating Jira ticket drafts (Bug, User Story, Epic, Task) — select appropriate template, fill with context from Jira/Confluence, generate structured draft, validate completeness."
compatibility: vscode
metadata:
  tools: mcp-atlassian, semantic_search, jira_search, confluence_search
  workflow: product-management
  related_skills: atlassian-ops, prd-writer
license: MIT
---

# Jira Ticket Writer Skill

Automated workflow untuk membuat Jira ticket drafts (Bug, User Story, Epic, Task) yang comprehensive dan consistent dengan standard templates.

## What I do

- Identify ticket type based on user request (Bug, User Story, Epic, Task)
- Search similar existing tickets untuk understand context & patterns
- Select appropriate template dari `/templates`
- Generate ticket draft dengan struktur yang konsisten
- Validate completeness dengan checklist
- Save draft to `/output` folder (READ-ONLY mode — no auto-creation in Jira)

## When to use me

Invoke skill ini ketika user meminta:

**Bug Tickets:**
- "Bikin draft bug ticket untuk [issue]"
- "Generate bug report untuk [problem]"
- "Draft tiket untuk bug [description]"

**User Stories:**
- "Bikin user story untuk [feature]"
- "Create story draft untuk [capability]"
- "Draft tiket story: As a [persona], I want [feature]"

**Epics:**
- "Bikin epic untuk [initiative]"
- "Draft epic ticket untuk [large feature]"
- "Create epic: [project name]"

**Tasks:**
- "Bikin task untuk [work item]"
- "Draft task ticket untuk [technical work]"
- "Create task: [description]"

## Workflow

### 1. **Discovery & Ticket Type Identification**

**Objective**: Understand ticket type dan gather relevant context

**Steps**:
```
a. Identify ticket type from user request
   - Bug: Problem/issue/defect yang perlu diperbaiki
   - User Story: Feature/capability untuk end user
   - Epic: Large initiative dengan multiple stories
   - Task: Technical/operational work item

b. Search similar existing tickets (optional)
   - Use jira_search untuk find similar tickets
   - Analyze structure dan detail level
   - Extract common patterns
   
c. Ask clarifying questions (if needed)
   - Summary/title
   - Description details
   - Priority/severity
   - Affected components
   - Known steps to reproduce (for bugs)
   - Acceptance criteria (for stories)
```

**Tools**: `jira_search`, `vscode_askQuestions`

---

### 2. **Template Selection**

**Objective**: Select appropriate template based on ticket type

**Template Mapping**:

| Ticket Type | Template File | Use Case |
|---|---|---|
| **Bug** | `templates/jira-bug-template.md` | Defects, issues, problems that need fixing |
| **User Story** | `templates/jira-user-story-template.md` | Feature requests, user-facing capabilities |
| **Epic** | `templates/jira-epic-template.md` | Large initiatives, multi-story projects |
| **Task** | `templates/jira-task-template.md` | Technical work, operational tasks, chores |

**Selection Logic**:
- User explicitly mentions type → use that template
- Description implies defect/problem → Bug template
- Description includes "As a user" → User Story template
- Description is large initiative → Epic template
- Description is technical work → Task template

---

### 3. **Content Generation**

**Objective**: Generate ticket draft menggunakan template structure

### Bug Ticket Generation

**Template**: `templates/jira-bug-template.md`

**Key Sections to Fill**:

1. **Basic Information**:
   - Issue Type: Bug
   - Project: [Auto-detect from context or ask]
   - Summary: [Clear, concise bug description]
   - Priority: [P0-P3 based on severity]
   - Severity: [Blocker/Critical/Major/Minor]
   - Labels: [bug], [affected-feature]
   - Affected Version: [Current version if known]

2. **Description**:
   - Bug Summary: 1-2 sentence clear description
   - Impact: Users affected, business impact, frequency
   - Steps to Reproduce: Numbered list of steps
   - Expected Behavior: What should happen
   - Actual Behavior: What actually happens

3. **Environment**:
   - Device/Browser details
   - OS version
   - Environment (Production/Staging/Dev)
   - URL where bug occurs

4. **Screenshots/Logs**:
   - Placeholder for screenshots
   - Console errors
   - Backend logs
   - Network requests

5. **Acceptance Criteria for Fix**:
   - Bug no longer reproduces
   - No regression in related features
   - Proper error handling added

**Example Output**:
```markdown
# Jira Bug Template

## Basic Information
- **Issue Type:** Bug
- **Project:** DPT
- **Summary:** Checkout button disabled when cart has valid items
- **Priority:** P1 (High)
- **Severity:** Major
- **Labels:** [bug], [checkout], [production]
- **Affected Version(s):** v2.5.3

## Description

### Bug Summary
Users report that the checkout button remains disabled even when they have valid items in their cart, preventing them from completing purchases.

### Impact
- **Users Affected:** ~5% of users (based on error logs)
- **Business Impact:** Revenue loss, cart abandonment increase
- **Frequency:** Intermittent (occurs ~30% of the time)

---

## Steps to Reproduce

1. Navigate to e-commerce site
2. Add 2-3 items to cart
3. Go to cart page
4. Click "Proceed to Checkout" button
5. Button remains disabled, no action occurs

---

## Expected Behavior
Checkout button should be enabled when cart has valid items, and clicking it should navigate to checkout page.

---

## Actual Behavior
Checkout button stays in disabled state (grayed out) despite valid cart items present.

---

## Environment

### Device/Browser
- **Device:** Desktop
- **OS:** Windows 11
- **Browser:** Chrome 120
- **Screen Resolution:** 1920x1080

### Environment
- **Environment:** Production
- **URL:** https://example.com/cart
- **Backend Version:** v2.5.3
- **Frontend Version:** v3.1.8

---

## Screenshots / Videos
[Attach screenshots showing disabled button with valid cart]

---

## Logs / Error Messages

### Console Errors
```
TypeError: Cannot read property 'enabled' of undefined
  at CartComponent.checkoutValidation (cart.js:145)
```

### Backend Logs
```
[No relevant backend errors found]
```

---

## Acceptance Criteria for Fix
- [ ] Checkout button enabled when cart has valid items
- [ ] Button click navigates to checkout page
- [ ] No console errors
- [ ] Fix tested on Chrome, Safari, Firefox
- [ ] Regression testing passed (add/remove items, empty cart)
```

---

### User Story Generation

**Template**: `templates/jira-user-story-template.md`

**Key Sections to Fill**:

1. **Basic Information**:
   - Issue Type: Story
   - Project: [From context]
   - Summary: As a [persona], I want [capability], so that [value]
   - Priority: [P0-P3]
   - Labels: [feature-name], [team-name]

2. **Description**:
   - User Story: As a... I want... So that...
   - Background/Context: Why is this needed?
   - Value Proposition: What value does it provide?

3. **Acceptance Criteria** (Given/When/Then format):
   - Scenario 1: Happy path
   - Scenario 2: Edge cases
   - Scenario 3: Error handling

4. **Technical Details**:
   - API Contract (if applicable)
   - Data Model Changes
   - Dependencies

5. **Testing Requirements**:
   - Unit tests
   - Integration tests
   - Manual QA checklist

6. **Definition of Done**:
   - Code complete and merged
   - Tests written and passing
   - QA tested
   - Documentation updated
   - Deployed to production

**Example Output**:
```markdown
# Jira User Story Template

## Basic Information
- **Issue Type:** Story
- **Project:** DPT
- **Summary:** As a customer, I want to save items to wishlist, so that I can purchase them later
- **Priority:** P2
- **Labels:** [wishlist], [customer-experience], [sprint-25]

## Description

### User Story
As a **customer**,  
I want **to save items to a wishlist**,  
So that **I can easily find and purchase them later without searching again**.

### Background / Context
Customers often browse products but aren't ready to purchase immediately. Without a wishlist feature, they have to manually search for items again, leading to frustration and lost sales.

### Value Proposition
- Increases customer retention (easier to return and purchase)
- Improves conversion rate (reduce friction in purchase journey)
- Provides data on customer intent (analytics on wished items)

---

## Acceptance Criteria

### Scenario 1: [Add item to wishlist]
**Given** I am viewing a product detail page,  
**When** I click the "Add to Wishlist" button,  
**Then** the item is saved to my wishlist and I see a confirmation message.

### Scenario 2: [View wishlist]
**Given** I have items in my wishlist,  
**When** I navigate to "My Wishlist" page,  
**Then** I see all saved items with product name, image, price, and "Add to Cart" button.

### Scenario 3: [Remove from wishlist]
**Given** I am viewing my wishlist,  
**When** I click "Remove" on an item,  
**Then** the item is removed from my wishlist immediately.

---

## Technical Details

### API Contract
```
POST /api/v1/wishlist
Request: { "product_id": "12345", "user_id": "67890" }
Response: { "success": true, "wishlist_id": "abc123" }

GET /api/v1/wishlist?user_id=67890
Response: { "items": [...], "total": 5 }

DELETE /api/v1/wishlist/{item_id}
Response: { "success": true }
```

### Data Model Changes
- New table: `wishlist` (id, user_id, product_id, created_at)
- Index on user_id for fast lookup

### Dependencies
- [ ] Database migration for wishlist table
- [ ] Analytics event tracking setup

---

## Definition of Done
- [ ] Code complete and merged to main
- [ ] Unit tests written and passing (>80% coverage)
- [ ] Integration tests passing
- [ ] Code reviewed by 2+ engineers
- [ ] QA tested on staging
- [ ] Documentation updated (API docs)
- [ ] Deployed to production
- [ ] Analytics tracking implemented

---

## Story Points
**Estimate:** 5
```

---

### Epic Generation

**Template**: `templates/jira-epic-template.md`

**Key Sections to Fill**:

1. **Basic Information**:
   - Issue Type: Epic
   - Epic Name: [Clear, action-oriented]
   - Summary: [One-line description]
   - Priority: [P0-P3]
   - Labels: [epic], [initiative-name]

2. **Description**:
   - Epic Overview: 2-3 sentence summary
   - Business Problem: What are we solving?
   - Target Users: Who benefits?

3. **Success Metrics**:
   - Table with Goal, Metric, Baseline, Target, Measurement Method

4. **Scope**:
   - In Scope: Features included
   - Out of Scope: What's not included

5. **User Stories** (Child Issues):
   - Must Have (MVP)
   - Should Have (Post-MVP)
   - Could Have (Nice to Have)

6. **Dependencies, Timeline, Risks**

---

### Task Generation

**Template**: `templates/jira-task-template.md`

**Key Sections to Fill**:

1. **Basic Information**:
   - Issue Type: Task
   - Summary: [Clear, action-oriented description]
   - Priority: [P0-P3]

2. **Description**:
   - Task Overview: What needs to be done
   - Why is this needed: Context
   - Expected Outcome: Deliverable

3. **Acceptance Criteria**: Checklist of outcomes

4. **Dependencies**: What blocks this or is blocked by this

5. **Time Estimate**: Story points or hours/days

---

### 4. **Validation Checklist**

**Objective**: Ensure ticket draft completeness

### Bug Ticket Checklist:
```
[ ] Summary is clear and describes the bug
[ ] Steps to reproduce are detailed and numbered
[ ] Expected vs Actual behavior clearly stated
[ ] Environment information complete (browser, OS, version)
[ ] Impact assessment included (users affected, frequency)
[ ] Priority/Severity assigned appropriately
[ ] Labels added for categorization
[ ] Acceptance criteria for fix defined
```

### User Story Checklist:
```
[ ] User story follows format: As a [persona], I want [capability], so that [value]
[ ] Background/context explains why it's needed
[ ] Acceptance criteria in Given/When/Then format
[ ] At least 3 scenarios covered (happy path, edge case, error)
[ ] Definition of Done checklist complete
[ ] Story points estimated
[ ] Dependencies identified
[ ] Technical details specified if applicable
```

### Epic Checklist:
```
[ ] Epic name is clear and action-oriented
[ ] Business problem well-defined
[ ] Success metrics with baseline and target
[ ] Scope clearly bounded (In Scope vs Out of Scope)
[ ] User stories listed (Must/Should/Could have)
[ ] Timeline and milestones defined
[ ] Dependencies identified
[ ] Risks documented with mitigation
```

### Task Checklist:
```
[ ] Task summary is action-oriented
[ ] Clear expected outcome/deliverable
[ ] Acceptance criteria defined
[ ] Dependencies listed
[ ] Time estimate provided
[ ] Technical details included if applicable
```

---

### 5. **Output & Delivery**

**Objective**: Save ticket draft to local file (READ-ONLY mode)

**File Naming Convention**:
```
output/ticket-[type]-[summary-slug]-[YYYYMMDD].md

Examples:
- output/ticket-bug-checkout-button-disabled-20260406.md
- output/ticket-story-wishlist-feature-20260406.md
- output/ticket-epic-mobile-app-rewrite-20260406.md
- output/ticket-task-update-dependencies-20260406.md
```

**Process**:
1. Generate complete ticket draft using template
2. Save to `/output` folder (NOT workspace root)
3. Show preview to user for review
4. If in READ-ONLY mode → provide instructions for manual Jira creation

**READ-ONLY Mode Behavior**:
```markdown
✅ Ticket draft generated: output/ticket-bug-checkout-disabled-20260406.md

⚠️ **READ-ONLY MODE ACTIVE**
I cannot create this ticket in Jira directly.

**To create manually:**
1. Open Jira: https://finacceljira.atlassian.net
2. Click "Create" button
3. Select project and issue type
4. Copy-paste content from the draft file above
5. Click "Create"

**Alternative:** If you want to enable write mode, see READ-ONLY-MODE.md
```

**If user asks to create in Jira**: Use **REFUSAL PROTOCOL** from senior-pm instructions.

---

## Integration with Other Tools

### Jira Search (Context Gathering)

**Before generating**, search for similar tickets:

```bash
jira_search(jql="project = DPT AND type = Bug AND summary ~ 'checkout'", max_results=5)
```

Use results to:
- Understand common patterns
- Check for duplicates
- Reference similar tickets in draft
- Adopt consistent language/terminology

### Confluence (Additional Context)

Search for related docs:
```bash
confluence_search(query="checkout flow documentation", limit=3)
```

Use to enrichcontext in ticket description.

---

## Example Prompts

**Bug Tickets**:
```
"Bikin bug ticket untuk checkout button yang tidak bisa diklik"
→ Asks clarifying questions → Generates bug draft with steps to reproduce

"Draft bug: mobile app crashes on iOS 17 saat login"
→ Auto-fills environment details → Generates comprehensive bug report
```

**User Stories**:
```
"Bikin user story untuk wishlist feature"
→ Generates story with Given/When/Then acceptance criteria

"Create story: As a PM, I want to export Jira data to CSV"
→ Includes technical details and API contract
```

**Epics**:
```
"Bikin epic untuk mobile app redesign project"
→ Generates epic with milestones, dependencies, success metrics

"Draft epic: Payment gateway integration"
→ Includes child stories breakdown (Must/Should/Could have)
```

**Tasks**:
```
"Bikin task untuk update Python dependencies"
→ Generates task with acceptance criteria and time estimate

"Draft task: Set up DataDog monitoring for API"
→ Includes technical details and configuration steps
```

---

## Error Handling & Fallbacks

**If template file not found**:
```
❌ Error: Template file not found: templates/jira-bug-template.md
→ Fallback: Generate basic structure from memory
→ Log warning to check template files
```

**If user provides minimal info**:
```
→ Use vscode_askQuestions to gather required fields
→ Generate with [TBD] placeholders for unknown items
→ Show draft and ask user to fill missing details
```

**If unsure about ticket type**:
```
→ Ask: "Is this a Bug (defect), User Story (feature), Epic (initiative), or Task (work item)?"
→ Default to Task if still unclear
```

---

## Quality Standards

**A good Bug ticket has**:
✅ Clear, specific summary
✅ Detailed steps to reproduce (numbered)
✅ Expected vs Actual behavior clearly stated
✅ Environment details (device, OS, browser, version)
✅ Impact assessment (users affected, business impact)
✅ Appropriate priority/severity
✅ Screenshots or error logs attached
✅ Acceptance criteria for fix

**A good User Story has**:
✅ Proper format: As a [persona], I want [capability], so that [value]
✅ Clear background/context
✅ Given/When/Then acceptance criteria
✅ Multiple scenarios (happy path, edge cases, errors)
✅ Definition of Done checklist
✅ Technical details (API contract, data model)
✅ Story point estimate
✅ Dependencies identified

**A good Epic has**:
✅ Clear business problem statement
✅ Success metrics with baselines and targets
✅ Well-defined scope (In/Out of Scope)
✅ Breakdown into child stories (Must/Should/Could have)
✅ Timeline with milestones
✅ Dependencies and risks documented
✅ Stakeholders identified

**A good Task has**:
✅ Action-oriented summary
✅ Clear expected outcome
✅ Acceptance criteria checklist
✅ Dependencies listed
✅ Time estimate
✅ Technical details if applicable

---

## Notes

- Always reference templates from `/templates` folder
- Search for similar tickets before generating (avoid duplicates)
- In READ-ONLY mode, always save to `/output` folder
- Use consistent language from existing tickets in the project
- Include both functional and non-functional requirements
- Add appropriate labels for categorization
- Link to related tickets/PRDs when relevant

## Related Skills

- **atlassian-ops**: For Jira search and operations
- **prd-writer**: Reference for comprehensive documentation patterns

## Changelog

- **2026-04-06 v1.0**: Initial version
  - Support for 4 ticket types: Bug, User Story, Epic, Task
  - Template-based generation
  - Comprehensive validation checklists
  - READ-ONLY mode support
  - Integration with Jira search for context gathering
