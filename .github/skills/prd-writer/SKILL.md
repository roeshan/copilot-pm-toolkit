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

**Common Structures**:

**A. Standard Feature PRD** (Pegasus-style):
```markdown
- Metadata table (Creation date, Jira epic, owners, status)
- Background | Context
  - Current state
  - Problem statement
  - Proposed solution
- Business Impact | Goals
  - Success metrics
  - Supporting metrics
- Technical Approach (optional)
- Timeline and Milestones
- Task and Acceptance Criteria
- Dependencies
- Out of Scope
- Open Questions
- References
- Appendix
```

**B. Experiment PRD** (ODS-style):
```markdown
- Metadata table
- Background | Context
  - Current performance
  - Hypothesis
- Experiment Goals
- Experiment Design
  - Control vs Treatment
  - User segmentation
  - Duration
- Success Metrics
- Task and Acceptance Criteria
- Dependencies
- References
```

**C. Model/ML PRD**:
```markdown
- Metadata table
- Background | Context
- Business Impact | Goals
- Technical Approach
  - Model architecture
  - Features
  - Training & deployment
- Model Output Specification
- A/B Testing Strategy
- Timeline and Milestones
- Task and Acceptance Criteria
- Risks & Mitigation
- References
```

---

### 3. **Content Generation**

**Objective**: Generate comprehensive PRD content

**Guidelines**:

**Metadata Table**:
```markdown
| Field | Value |
|-------|-------|
| Creation Date | [Current date] |
| Jira Epic | [Link or TBD] |
| Target release | [Quarter/Month Year] |
| Doc Owner | @[Name] |
| Doc Reviewer | [TBD or Name] |
| MLE/Engineer | [TBD or Name] |
| QA | [TBD or Name] |
| DS | [TBD or Name] |
| Priority | P0/P1/P2 |
| Document status | DRAFT/IN REVIEW/APPROVED |
| Stakeholder | @[Name] |
```

**Writing Style**:
- **Professional yet collaborative** tone
- **Data-driven**: Include metrics, dashboards, references
- **Specific**: Avoid vague terms like "improve performance" → use "reduce latency by 30%"
- **Actionable**: Clear acceptance criteria
- **Complete**: Address all sections, use "TBD" if unknown

**Section Tips**:

1. **Background**: 
   - Current state with metrics
   - Clear problem statement
   - Why now? (urgency/timing)

2. **Success Metrics**:
   - Table format: Metric | Current | Target | Measurement Method
   - Primary + supporting metrics
   - Include statistical significance requirements

3. **Task & Acceptance Criteria**:
   - Table format: Task | PIC | Acceptance Criteria | Jira Link | Status
   - Specific, testable criteria
   - Clear ownership

4. **Timeline**:
   - Phase-based or milestone-based
   - Include deliverables per phase
   - Realistic estimates

5. **Risks & Mitigation**:
   - Table: Risk | Impact | Mitigation
   - Technical, resource, timeline risks
   - Dependencies as risks

6. **Open Questions**:
   - Table: Question | Answer | Date Answered | Decision Owner
   - Use [TBD] for unanswered
   - Update as answered

---

### 4. **Validation Checklist**

**Objective**: Ensure PRD completeness sebelum publish

**Checklist**:
```
[ ] Metadata complete (at minimum: owner, target release, status)
[ ] Background explains current state & problem clearly
[ ] Success metrics are specific & measurable
[ ] Timeline has realistic milestones
[ ] Tasks have clear acceptance criteria
[ ] Dependencies identified
[ ] Risks documented with mitigation
[ ] References linked (Jira, dashboards, related docs)
[ ] Writing is clear & free of jargon
[ ] Technical details sufficient for engineering
[ ] Business justification clear for stakeholders
```

**Red Flags** (fix these):
- ❌ Vague success metrics ("improve user experience")
- ❌ Missing acceptance criteria
- ❌ No timeline or milestones
- ❌ "Will discuss later" without action items
- ❌ Technical approach missing for complex features
- ❌ No risk assessment

---

### 5. **Output & Delivery**

**Objective**: Deliver PRD in appropriate format

**Options**:

**A. Markdown Draft** (Default):
- Generate complete markdown
- Show to user for review
- Save to workspace if requested

**B. Confluence Page**:
- Convert to Confluence storage format
- Use `confluence_create_page` with:
  - `space_key`: (e.g., "DS")
  - `parent_id`: (e.g., 3507979471 for PRD Pegasus)
  - `title`: Follow naming convention (e.g., "[KID] PRD - 202604 - TEAM - Feature Name")
  - `emoji`: Appropriate emoji (🚀📋📊🤖)

**C. Local File**:
- Save as `.md` file in workspace
- Suggested location: `/docs/prds/` or `/prd/`

**Always**:
- Show draft first untuk review
- Ask user preference: "Want me to upload to Confluence now, or review first?"
- After upload, provide Confluence link

---

## Naming Conventions

**Confluence Pages**:
```
[PREFIX] - [PROJECT] - [DESCRIPTION] - [DATE]

Prefixes:
- [KID] = Kredivo Indonesia
- [ODS] = One-page Design Spec  
- [RFC] = Request for Comments
- [EXP] = Experiment

Examples:
- [KID] PRD - 202604 - Pegasus - Buy Again Model
- [ODS] - Pegasus - Biller Recommendation Experiment - 20250211
- [RFC] - Backend - New Payment Gateway Integration
```

**File Names** (if saving locally):
```
prd-[project]-[feature]-[yyyymmdd].md

Examples:
- prd-pegasus-buy-again-model-20260401.md
- prd-checkout-discount-code-20260315.md
```

---

## Templates by Type

### Template 1: Standard Feature PRD

Use for: New features, enhancements, major changes

**Key Sections**:
- Background | Context
- Business Impact | Goals  
- Timeline and Milestones
- Task and Acceptance Criteria
- Dependencies
- Risks & Mitigation
- References

### Template 2: Experiment/A/B Test PRD

Use for: Experiments, A/B tests, hypothesis validation

**Key Sections**:
- Background | Context (with Current Performance)
- Experiment Goals
- Experiment Design (Control vs Treatment)
- Success Metrics
- Task and Acceptance Criteria
- References

### Template 3: ML/Model PRD

Use for: Machine learning models, data science projects

**Key Sections**:
- Background | Context
- Business Impact | Goals
- Technical Approach (Model Architecture, Features, Training)
- Model Output Specification
- A/B Testing Strategy
- Timeline and Milestones
- Task and Acceptance Criteria
- Risks & Mitigation

### Template 4: ODS (One-Page Design Spec)

Use for: Quick specs, simple features, small experiments

**Key Sections**:
- Metadata table
- Background (1-2 paragraphs)
- Goals (bullet points)
- Design/Approach (brief)
- Success Metrics
- Timeline
- References

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

**A good PRD has**:
✅ Clear problem statement & solution
✅ Measurable success metrics
✅ Specific acceptance criteria
✅ Realistic timeline
✅ Identified risks & mitigation
✅ Complete references
✅ Proper formatting (tables, sections, links)

**Common Issues to Avoid**:
❌ Vague requirements
❌ Missing success metrics
❌ No timeline
❌ Unclear ownership
❌ Incomplete technical details
❌ No risk assessment
❌ Poor formatting

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

- 2026-04-01: Initial version based on Pegasus PRD analysis
