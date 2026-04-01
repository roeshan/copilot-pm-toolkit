---
name: prd-writer
description: "Use when: creating Product Requirement Documents (PRD) — search existing PRDs for context, analyze structure, generate draft with proper format, validate completeness, and optionally publish to Confluence."
compatibility: vscode
metadata:
  tools: mcp-atlassian, semantic_search, confluence_search
  workflow: product-management
  related_skills: atlassian-ops
license: MIT
---

# PRD Writer Skill

Automated workflow untuk membuat Product Requirement Document (PRD) yang comprehensive dan consistent dengan standard yang ada.

## What I do

- Search and analyze existing PRDs untuk understand format & context
- Generate PRD draft dengan struktur yang konsisten
- Validate completeness dengan checklist
- Format untuk Confluence atau Markdown
- Optional: Upload langsung ke Confluence space

## When to use me

Invoke skill ini ketika user:
- "Bikin PRD untuk [feature name]"
- "Create PRD [project name]"
- "Tulis dokumen requirement untuk [initiative]"
- "Generate PRD [feature] di Confluence"

## Workflow

### 1. **Discovery & Context Gathering**

**Objective**: Understand existing format dan gather relevant context

**Steps**:
```
a. Identify PRD type & target audience
   - Product feature PRD
   - Experiment/A/B test PRD  
   - Technical RFC-style PRD
   - ODS (One-page Design Spec)

b. Search existing PRDs
   - Use confluence_search dengan keywords
   - Check parent page structure
   - Identify naming convention
   
c. Analyze 1-2 existing PRDs
   - Read full content dari similar PRD
   - Extract metadata structure
   - Note sections, tone, detail level
   
d. Ask clarifying questions
   - Feature name & objective
   - Target release timeline
   - Known stakeholders
   - Success metrics (if known)
```

**Tools**: `confluence_search`, `confluence_get_page`, `vscode_askQuestions`

---

### 2. **Structure Definition**

**Objective**: Define PRD outline berdasarkan type & context

**Standard PRD Structure** (Template v2):

Based on official template: https://finacceljira.atlassian.net/wiki/spaces/DS/pages/5430511189

```markdown
# PRD – [Tribe] – [Product Name] – [Feature Title]

## Metadata Table
- Creation Date, Jira Epic, Target Release
- Doc Owner, Reviewers, Status
- GTM Link, Tech Doc
- DS, MLE, QA, Product contacts
- Priority (P0-P3)

## 🎯 Objective / Problem Statement
- Background (current state/context)
- Problem Statement (user-focused, clear)
- Goals (what success looks like)
- Non-Goals / Out of Scope (high level)

## 👥 Target Personas / Market / Stakeholders
- Primary & Secondary Personas
- Internal Stakeholders (Ops, CS, Sales)
- Profile, needs, key behaviors for each

## 📊 Success Metrics / Business Impact
- Goal | Metric | Current Baseline | Target | Measurement Method
- Both primary and supporting metrics
- Clear data sources (Analytics, logs, surveys)

## 🤔 Assumptions
- What must be true for solution to work
- User, Tech, Business assumptions
- Validation plan for each

## 👥 Dependencies
- Task/Deliverable | Owner (Squad/Team) | Due Date | Status | Notes
- Cross-team dependencies clearly identified

## 🌟 Milestones
- M1: Discovery/Alignment
- M2: Design Complete
- M3: Dev Complete
- M4: Launch/GA
- Each with: Description, Target Date, Owner, Status, Jira Ticket

## 📝 Requirements
### 1. Scope Overview
- In Scope (feature areas)
- Out of Scope (for this release)

### 2. Prerequisites
- Infra/BFF/Platform requirements
- Data/Events requirements
- Related docs

### 3. Feature Requirements
For each feature:
- Summary
- User Story table (Requirement | User Story | Notes | Visuals)
- High Level Flow
- Data & Feature Definition (for ML/DS projects)
- Acceptance Criteria:
  * UX Flow & UI Behavior
  * Logic & Business Rules
  * Data Tracking (events, properties, A/B test)
  * Squad Scope (FE/BE/DS responsibilities)
- Experiment Design (if A/B testing needed)

## ❓ FAQ
- Why this approach vs alternatives?
- How does this interact with existing features?
- What happens if this fails?

## ⚠️ Detailed Out of Scope
- Product/UX exclusions
- Tech exclusions
- Reasons & future considerations

## ❓ Open Questions
- Question | Owner | Answer | Date Answered
- Track unresolved items with "TBD"

## 📝 Reference
- PRDs from other teams
- Analysis documents
- Research & benchmarks

## 📝 API Contract
- Technical specifications
- Request/Response formats
- Integration details
```

**Variant Structures**:

**For Experiments/A/B Tests**: 
- Emphasize "Experiment Design" section in Feature Requirements
- Add detailed control vs treatment comparison
- Include statistical significance requirements

**For ML/DS Projects**: 
- Add "Data & Feature Definition" section
- Include "Model Output Specification"
- Detail training/deployment approach
- Add model monitoring requirements

---

### 3. **Content Generation**

**Objective**: Generate comprehensive PRD content

**Guidelines**:

**Metadata Table** (Template v2):
```markdown
| Field | Value |
|-------|-------|
| **Creation Date** | [YYYY-MM-DD] |
| **Jira Epic** | [Link to epic or TBD] |
| **Target release** | [Q# YYYY or specific date] |
| **Doc Owner** | [Name / Squad] |
| **Doc Reviewer(s)** | [Name(s)] |
| **Document status** | DRAFT / REVIEW / APPROVED |
| **GTM Link** | [Link to GTM/launch plan or TBD] |
| **Tech Doc** | [Link to tech/architecture doc or TBD] |
| **DS** | [Primary DS contact or TBD] |
| **MLE** | [Primary MLE contact or TBD] |
| **QA** | [Primary QA contact or TBD] |
| **Product** | [PM / PO name] |
| **Priority** | P0 / P1 / P2 / P3 |
```

**Writing Style**:
- **Professional yet collaborative** tone
- **Data-driven**: Include metrics, dashboards, references
- **Specific**: Avoid vague terms like "improve performance" → use "reduce latency by 30%"
- **User-focused**: Start with user problem, not technical solution
- **Actionable**: Clear acceptance criteria with measurable outcomes
- **Complete**: Address all sections, use "TBD" if unknown

**Section-by-Section Tips**:

**1. 🎯 Objective / Problem Statement**:
```markdown
### Background:
- Describe current state with metrics
- Explain market/user context
- Why this matters now (urgency/timing)

### Problem Statement:
- One clear, user-focused problem
- "Users struggle with X because Y, resulting in Z"

### Goals:
- 2-4 specific, measurable goals
- What success looks like

### Non-Goals:
- Explicitly list what we WON'T do
- Prevent scope creep
```

**2. 👥 Target Personas / Market / Stakeholders**:
```markdown
| Type of persona | Profile |
|---|---|
| Primary: [User type] | [Brief description, needs, behaviors] |
| Secondary: [User type] | [Description] |
| Internal: Ops Team | [How they're impacted] |
```

**3. 📊 Success Metrics / Business Impact**:
```markdown
| Goal / Area | Metric | Current Baseline | Target | Measurement Method |
|---|---|---|---|---|
| Engagement | CTR | 1.5% | 3.0% | Amplitude dashboard |
| Conversion | Purchase rate | 0.8% | 1.5% | Transaction logs |
| Performance | API latency p95 | 500ms | 200ms | DataDog monitoring |
```

**4. 🤔 Assumptions**:
```markdown
| Area | Assumption | Validation Plan |
|---|---|---|
| User | "Users prefer X over Y" | A/B test or user survey |
| Tech | "Infra can handle 2x traffic" | Load test |
| Business | "Partners will adopt API v2" | Pilot with 2 partners |
```

**5. 👥 Dependencies**:
```markdown
| Task / Deliverable | Owner (Squad/Team) | Due Date | Status | Notes |
|---|---|---|---|---|
| New API endpoint | Backend Team | 2026-05-01 | IN PROGRESS | Blocked on infra |
| ML model training | DS Team | 2026-04-20 | NOT STARTED | Waiting for data |
```

**6. 🌟 Milestones**:
```markdown
| Milestone | Description | Target Date | Owner | Status | Jira Ticket |
|---|---|---|---|---|---|
| M1: Discovery | Requirements gathering, design | 2026-04-15 | PM Team | DONE | [EPIC-123] |
| M2: Design Complete | UX finalized, specs ready | 2026-05-01 | Design | IN PROGRESS | [EPIC-124] |
| M3: Dev Complete | Code complete, ready for QA | 2026-06-01 | Eng | NOT STARTED | [EPIC-125] |
| M4: Launch | Feature live in prod | 2026-06-15 | All | NOT STARTED | [EPIC-126] |
```

**7. 📝 Requirements - Feature Requirements**:

For each feature:
```markdown
#### Feature #1 – [Feature Name]

**Summary**
[2-3 sentence description]

| Requirement | User Story | Notes | New Visual | Old Visual |
|---|---|---|---|---|
| REQ-1: [Title] | As a [persona], I want [capability], so that [value] | [Edge cases, clarifications] | [Figma link] | [Screenshot or N/A] |

**High Level Flow**
[Diagram or bullet-point flow]

**Data & Feature Definition** (for ML/DS projects)
- Input features: [list]
- Model type: [e.g., XGBoost, Neural Net]
- Refresh cadence: [e.g., daily batch]

**Acceptance Criteria**

*UX Flow & UI Behavior*
1. Element placement: [Where it appears, visibility rules]
2. Interactions: [Click, tap, hover behavior]
3. Performance: [Load time < X ms]

*Logic & Business Rules*
1. Input → output mapping
2. Configurable parameters (thresholds, limits)
3. Error handling & fallback behavior

*Data Tracking*
1. Track `feature_clicked` when user clicks CTA
2. Log properties: {item_id, position, variant}
3. A/B test: 50/50 split by user_id suffix

*Squad Scope*
- **Platform Front-End**: Rendering, validation, tracking
- **Platform Back-End**: API contracts, business logic, configs
- **Data Science / MLE**: Model API, ranking, monitoring

**Experiment Design** (if applicable)
- Control: Existing behavior
- Treatment: New feature enabled
- Split: 50/50 by user suffix
- Duration: 4 weeks
- Success criteria: CTR improvement > 30%, p < 0.05
```

**8. ❓ Open Questions**:
```markdown
| Question | Owner | Answer | Date Answered |
|---|---|---|---|
| What's min data requirement per user? | DS Team | TBD | - |
| How to handle API downtime? | MLE Team | Fallback to cached data | 2026-04-02 |
```

**Common Mistakes to Avoid**:
- ❌ Vague problem statement ("improve UX")
- ❌ Success metrics without baseline
- ❌ User stories without acceptance criteria
- ❌ Missing squad responsibilities
- ❌ No validation plan for assumptions
- ❌ Incomplete metadata (missing owners/dates)

---

### 4. **Validation Checklist**

**Objective**: Ensure PRD completeness sebelum publish

**Checklist** (based on Template v2):
```
Metadata & Setup
[ ] All metadata fields filled (at minimum: owner, reviewers, target release, status)
[ ] Jira Epic linked (or marked TBD with follow-up plan)
[ ] GTM Link provided (or marked TBD if not applicable)
[ ] Priority level assigned (P0-P3)

Problem & Goals
[ ] Problem statement is clear and user-focused
[ ] Background explains current state with data/metrics
[ ] Goals are specific and measurable (not "improve UX")
[ ] Non-Goals explicitly listed to prevent scope creep

Personas & Impact
[ ] Target personas identified (primary & secondary)
[ ] Internal stakeholders listed with their roles
[ ] Success metrics have current baseline AND target
[ ] Measurement method specified for each metric

Assumptions & Dependencies
[ ] Key assumptions documented with validation plans
[ ] Cross-team dependencies identified with owners
[ ] Dependency due dates are realistic
[ ] Dependency status tracked

Requirements & Features
[ ] Scope clearly defined (In Scope vs Out of Scope)
[ ] Each feature has user stories with acceptance criteria
[ ] UX/UI behavior specified (placement, interactions, states)
[ ] Business logic documented (rules, configs, fallbacks)
[ ] Data tracking events defined (event names, properties)
[ ] Squad responsibilities clear (FE/BE/DS/QA scope)
[ ] Experiment design included if A/B testing required

Timeline & Milestones
[ ] Milestones are realistic and achievable
[ ] Each milestone has owner, date, status
[ ] Jira tickets linked to milestones

Documentation
[ ] FAQ addresses common questions
[ ] Open Questions tracked with owners
[ ] References linked (related PRDs, docs, dashboards)
[ ] API Contract documented if applicable
```

**Quality Gates** (must pass before APPROVED status):

**🟢 READY FOR REVIEW**:
- All metadata complete
- Problem statement & goals clear
- Success metrics defined
- Feature requirements outlined

**🟡 IN REVIEW**:
- Feedback from reviewers addressed
- Open questions answered or escalated
- Dependencies confirmed with teams
- Experiment design validated (if applicable)

**🔴 APPROVED**:
- All acceptance criteria validated
- GTM plan linked and aligned
- Tech doc available
- Launch readiness confirmed

**Red Flags** (fix before proceeding):
- ❌ Vague success metrics ("improve user experience", "increase engagement")
- ❌ Missing acceptance criteria for features
- ❌ No timeline or unrealistic timeline
- ❌ "Will discuss later" without concrete action items
- ❌ Squad scope unclear (who builds what?)
- ❌ No assumptions documented
- ❌ Missing data tracking requirements
- ❌ No validation plan for critical assumptions
- ❌ Circular dependencies without mitigation

---

### 5. **Output & Delivery**

**Objective**: Deliver PRD in appropriate format

**Options**:

**A. Local Markdown File** (Default for READ-ONLY mode):
- Generate complete markdown
- **Save to `/output` folder** with naming convention:
  - `output/prd-[team]-[product]-[feature]-[YYYYMMDD].md`
  - Example: `output/prd-ds-pegasus-buy-again-model-20260401.md`
- Show to user for review
- Reference template from `/templates/prd-template.md`

**B. Confluence Page** (DISABLED in READ-ONLY mode):
- ❌ `confluence_create_page` is DISABLED
- User must manually copy-paste to Confluence
- Provide instructions: "Copy content from `output/[filename].md` and paste to Confluence"

**C. Draft for Manual Upload**:
- Save to `/output` folder
- Provide Confluence URL and space key
- User manually creates page

**Always**:
- Show draft first untuk review
- Save to `/output` folder (NOT workspace root)
- Follow naming convention: `prd-[team]-[product]-[feature]-[YYYYMMDD].md`
- If asked to upload: Use **REFUSAL PROTOCOL** (READ-ONLY mode)

---

## Naming Conventions

**Confluence Pages** (Template v2 format):
```
[Tribe] – [Product Name] – [Feature Title] – [YYYYMMDD]

Examples:
- KID – Pegasus – Buy Again Model – 20260401
- ODS – Pegasus – Biller Recommendation Experiment – 20250211
- GRO – Checkout – Discount Code Feature – 20260315
- DS – Analytics – User Segmentation API – 20260420

Tribes/Teams:
- KID = Kredivo Indonesia
- ODS = One-page Design Spec
- GRO = Growth Team
- DS = Data Services
- DT = Data Team
- ENG = Engineering
- PRD = Product (general)
```

**Alternative Format** (Legacy, still acceptable):
```
[PREFIX] PRD - YYYYMM - [TEAM] - [Feature Name]

Examples:
- [KID] PRD - 202604 - Pegasus - Buy Again Model
- [ODS] - Pegasus - Biller Recommendation Experiment - 20250211
- [RFC] - Backend - New Payment Gateway Integration
```

**File Names** (if saving locally):
```
output/prd-[team]-[product]-[feature]-[yyyymmdd].md

Examples:
- output/prd-ds-pegasus-buy-again-model-20260401.md
- output/prd-kid-checkout-discount-code-20260315.md
- output/prd-gro-analytics-user-segmentation-20260420.md
```

**Templates Location:**
- Reference template: `templates/prd-template.md`
- All templates stored in `/templates` folder
- prd-growth-checkout-discount-code-20260315.md
- prd-mle-ranking-model-v2-20260420.md
```

**Best Practice**: 
- Use Template v2 format for new PRDs in Confluence
- Keep legacy format for backward compatibility if needed
- Always include date for version tracking

---

## Official Template

**Template v2**: https://finacceljira.atlassian.net/wiki/spaces/DS/pages/5430511189

Use this as the canonical structure for ALL PRDs unless explicitly told otherwise.

### When to Adapt the Template:

**For Standard Features**:
- Use full template as-is
- Include all sections
- Focus on "Feature Requirements" with detailed acceptance criteria

**For Experiments/A/B Tests**:
- Emphasize "Experiment Design" in Feature Requirements section
- Add detailed control vs treatment comparison
- Include:
  - User segmentation method
  - Sample size calculation
  - Duration & stopping criteria
  - Statistical significance threshold
  - Rollback plan

**For ML/Data Science Projects**:
- Add "Data & Feature Definition" subsection in Feature Requirements
- Include:
  - Input features & data sources
  - Model architecture choice
  - Training/evaluation approach
  - Inference method (batch/real-time)
  - Model monitoring requirements
  - Performance benchmarks

**For Quick Specs/Small Features**:
- Can simplify some sections (e.g., combine Personas into Problem Statement)
- But still maintain core structure:
  - Metadata
  - Objective/Problem
  - Success Metrics
  - Requirements with Acceptance Criteria
  - Open Questions

**For Technical/Infrastructure Projects**:
- Emphasize "Prerequisites" section
- Add detailed "API Contract" section
- Include architecture diagrams in Requirements
- Focus on non-functional requirements (performance, security, scalability)

### Customization Guidelines:

✅ **DO**:
- Add sections if project needs them (e.g., "Security Requirements", "Data Privacy")
- Expand Feature Requirements with project-specific details
- Include relevant diagrams, mockups, data flows
- Add more rows to tables as needed

❌ **DON'T**:
- Skip required sections (Metadata, Objective, Success Metrics, Requirements)
- Remove key fields from Metadata table
- Omit Acceptance Criteria
- Skip Data Tracking requirements

---

## Integration with Other Tools

### Jira Integration

**Best Practices**:
- Link Jira Epic in metadata table
- Create Epic first, then reference in PRD
- Use consistent naming: PRD title should match Epic summary
- Track tasks in Jira, reference tickets in PRD

**Epic Link Format**:
```markdown
| **Jira Epic** | [DDT-123](https://finacceljira.atlassian.net/browse/DDT-123) |
```

### Confluence Integration

**Space Mapping**:
- **DS** (Data Services): Pegasus, ML models, data pipelines
- **DT** (Data Team): Technical docs, API contracts
- **Product**: Product strategy, roadmaps
- **Engineering**: Technical RFCs, architecture

**Parent Pages** (common):
- PRD Pegasus: `3507979471`
- (Check confluence_search untuk find others)

### Amplitude/Analytics

**Include in References**:
- Link to relevant dashboards
- Define tracking events in Appendix
- Map events to success metrics

---

## Example Prompts

**Simple**:
```
"Bikin PRD untuk buy again model di Pegasus"
→ Triggers discovery, searches existing Pegasus PRDs, generates ML-style PRD
```

**With Details**:
```
"Create PRD for discount code feature in checkout. 
Target: Q2 2026. Owner: John. Success metric: 20% increase in conversion."
→ Generates feature PRD with provided details
```

**Experiment**:
```
"Buat experiment PRD untuk test new homepage layout. 
Control vs treatment, 50-50 split, run 4 weeks."
→ Generates experiment/A/B test style PRD
```

**Update Existing**:
```
"Update PRD [link] dengan task baru untuk backend integration"
→ Reads existing, adds section, updates
```

---

## Error Handling & Fallbacks

**If Confluence search fails**:
- Use local template from workspace
- Ask user for example PRD link
- Proceed with generic template

**If user provides minimal info**:
- Use `vscode_askQuestions` to gather:
  - Feature name
  - Objective/goal
  - Target timeline
  - Stakeholders
- Generate with placeholders ([TBD]) for unknown info

**If unsure about format**:
- Default to Standard Feature PRD template
- Show draft, ask if format needs adjustment

---

## Quality Standards

**A good PRD (Template v2) has**:
✅ Complete metadata (all owners, dates, links identified)
✅ Clear, user-focused problem statement
✅ Measurable success metrics with baselines & targets
✅ Well-defined personas & stakeholders
✅ Documented assumptions with validation plans
✅ Cross-team dependencies tracked
✅ Detailed feature requirements with acceptance criteria
✅ UX/UI behavior specified
✅ Business logic documented
✅ Data tracking requirements defined
✅ Squad responsibilities clear (FE/BE/DS scope)
✅ Realistic timeline with milestones
✅ FAQ addresses common questions
✅ Open questions tracked with owners
✅ Complete references (Jira, docs, dashboards)
✅ API contract documented (if applicable)
✅ Proper formatting (tables, sections, emojis, links)

**Common Issues to Avoid**:
❌ Vague requirements ("improve UX", "make it better")
❌ Success metrics without baseline or measurement method
❌ Missing squad scope (who builds what?)
❌ No data tracking requirements
❌ Unclear timeline or missing milestones
❌ Assumptions not validated
❌ Dependencies without due dates or owners
❌ User stories without acceptance criteria
❌ No experiment design for A/B tests
❌ Missing GTM plan for launches
❌ Incomplete technical documentation
❌ Poor formatting (no tables, broken links)
❌ Document status not updated (stuck in DRAFT)

**Review Checklist** (before moving to APPROVED):
1. All reviewers have provided feedback
2. Open questions answered or escalated
3. Dependencies confirmed with owning teams
4. Success metrics validated by analytics
5. Technical feasibility confirmed by engineering
6. GTM plan aligned with timeline
7. QA test plan discussed
8. Launch readiness criteria defined

---

## Notes

- Always search existing PRDs first untuk maintain consistency
- When in doubt, ask clarifying questions
- Default to showing draft before publishing
- Keep PRD concise but complete
- Use tables for structured data
- Link extensively (Jira, dashboards, related docs)
- Update "Document status" as PRD evolves (DRAFT → IN REVIEW → APPROVED)

## Related Skills

- **atlassian-ops**: For Confluence/Jira operations
- **agent-customization**: If need to create project-specific PRD templates

## Changelog

- **2026-04-01 v2.0**: Updated to Template v2 structure
  - Adopted official template: https://finacceljira.atlassian.net/wiki/spaces/DS/pages/5430511189
  - Added comprehensive metadata fields (GTM Link, Tech Doc)
  - Restructured sections with emoji headers (🎯 📊 👥 etc.)
  - Enhanced Feature Requirements format with detailed acceptance criteria
  - Added Personas, Assumptions, FAQ sections
  - Improved validation checklist for quality gates
  - Removed old template variants, unified on single standard
  
- **2026-04-01 v1.0**: Initial version based on Pegasus PRD analysis
