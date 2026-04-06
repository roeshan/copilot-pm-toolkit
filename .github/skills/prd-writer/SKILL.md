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

**Objective**: Define PRD outline berdasarkan existing template

**Standard PRD Structure** (based on `/templates/prd-template.md`):

```markdown
# Product Requirements Document (PRD)

## 1. Document Title & Version
- **Product Name:**
- **Document Version:**
- **Date:**
- **Author:**

## 2. Executive Summary
Brief overview of the product, its purpose, and the value it brings.

## 3. Background & Objectives
- **Background:**
  - Context and reasons for building the product.
- **Objectives:**
  - Clear goals the product aims to achieve.

## 4. Product Scope
- **In Scope:**
  - Features and functionalities included in this release.
- **Out of Scope:**
  - Features and functionalities not included.

## 5. Key Features & Functional Requirements
List and describe the main features and their functional requirements.
- **Feature 1:**
  - Description:
  - Requirements:
- **Feature 2:**
  - Description:
  - Requirements:

## 6. Non-Functional Requirements
- Performance
- Security
- Usability
- Scalability
- Compliance

## 7. User Stories / Use Cases
Describe how different users will interact with the product.
- **User Story 1:**
- **User Story 2:**

## 8. Success Criteria / Acceptance Criteria
Define what success looks like for this product or feature.
- **Criterion 1:**
- **Criterion 2:**

## 9. Timeline & Milestones
Outline the key phases and expected delivery dates.
- **Milestone 1:**
- **Milestone 2:**

## 10. Risks & Mitigation
Identify potential risks and how to address them.
- **Risk 1:**
  - Mitigation:
- **Risk 2:**
  - Mitigation:

## 11. Appendix
Include any additional information, diagrams, or references.
```

**Template Variations**:

**For Complex Features**: 
- Expand "Key Features & Functional Requirements" with detailed subsections
- Add data flow diagrams in Appendix
- Include API specifications if needed

**For Experiments/A/B Tests**: 
- Add "Experiment Design" subsection under Features
- Include control vs treatment comparison
- Specify statistical significance requirements

**For ML/DS Projects**: 
- Add "Data Requirements" under Non-Functional Requirements
- Include model specifications in Features section
- Detail training/deployment approach in Timeline

---

### 3. **Content Generation**

**Objective**: Generate comprehensive PRD content following standard template

**Writing Style**:
- **Professional yet collaborative** tone
- **Data-driven**: Include metrics, dashboards, references
- **Specific**: Avoid vague terms like "improve performance" → use "reduce latency by 30%"
- **User-focused**: Start with user problem, not technical solution
- **Actionable**: Clear acceptance criteria with measurable outcomes
- **Complete**: Address all sections, use "TBD" if unknown

**Section-by-Section Tips**:

**1. Document Title & Version**:
```markdown
- **Product Name:** [Feature/Product Name]
- **Document Version:** v1.0
- **Date:** [YYYY-MM-DD]
- **Author:** [PM Name / Team]
```

**2. Executive Summary**:
- Brief overview (2-3 paragraphs)
- What the product is
- Why it's being built
- Key value proposition

**3. Background & Objectives**:
```markdown
**Background:**
- Current state with metrics/data
- Market/user context
- Why this matters now

**Objectives:**
- 3-5 specific, measurable goals
- What success looks like
```

**4. Product Scope**:
```markdown
**In Scope:**
- Feature/functionality 1
- Feature/functionality 2
- Feature/functionality 3

**Out of Scope:**
- Explicitly list what we WON'T do
- Prevent scope creep
- Future considerations
```

**5. Key Features & Functional Requirements**:
```markdown
**Feature 1: [Name]**
- **Description:** [What it does, why it's needed]
- **Requirements:**
  - Functional requirement 1
  - Functional requirement 2
  - User interactions and flows
  - Edge cases to handle

**Feature 2: [Name]**
- [Same structure]
```

**6. Non-Functional Requirements**:
- **Performance**: Load time < X ms, handles Y concurrent users
- **Security**: Authentication, data encryption, compliance (GDPR, etc.)
- **Usability**: Accessibility standards, mobile responsive
- **Scalability**: Can handle 2x traffic growth
- **Compliance**: Regulatory requirements

**7. User Stories / Use Cases**:
```markdown
**User Story 1:**
As a [persona],
I want [capability],
So that [business value].

**Acceptance Criteria:**
- Given [precondition]
- When [action]
- Then [expected result]
```

**8. Success Criteria / Acceptance Criteria**:
```markdown
**Criterion 1:** [Specific, measurable outcome]
- Metric: [e.g., CTR increases from 1.5% to 3.0%]
- Measurement: [Dashboard/tool used]

**Criterion 2:** [Another measurable outcome]
```

**9. Timeline & Milestones**:
```markdown
**Milestone 1: Discovery** (Target: [Date])
- Requirements gathering
- Stakeholder alignment

**Milestone 2: Design Complete** (Target: [Date])
- UX/UI finalized
- Technical specs ready

**Milestone 3: Development Complete** (Target: [Date])
- Code complete, ready for QA

**Milestone 4: Launch** (Target: [Date])
- Feature live in production
```

**10. Risks & Mitigation**:
```markdown
**Risk 1:** [Description]
- **Impact:** High/Medium/Low
- **Probability:** High/Medium/Low
- **Mitigation:** [How to address]

**Risk 2:** [Description]
- [Same structure]
```

**11. Appendix**:
- Wireframes/mockups
- API specifications
- Data schemas
- Research findings
- Related PRDs
- Meeting notes

**Common Mistakes to Avoid**:
- ❌ Vague objectives ("improve UX" without metrics)
- ❌ Success criteria without measurement method
- ❌ User stories without acceptance criteria
- ❌ Missing non-functional requirements
- ❌ Unrealistic timelines
- ❌ No risk mitigation plans

---

### 4. **Validation Checklist**

**Objective**: Ensure PRD completeness sebelum publish

**Checklist** (based on `/templates/prd-template.md`):

```
Document Setup
[ ] Product name and version clearly specified
[ ] Date and author documented
[ ] Document is properly titled

Executive Summary
[ ] Brief overview of product/feature (2-3 paragraphs)
[ ] Purpose and value clearly stated

Background & Objectives
[ ] Background explains current state with context
[ ] Objectives are specific and measurable (not vague like "improve UX")
[ ] Clear business/user need identified

Product Scope
[ ] In Scope items clearly listed
[ ] Out of Scope explicitly documented to prevent scope creep
[ ] Scope boundaries are realistic

Key Features & Functional Requirements
[ ] All major features documented
[ ] Each feature has clear description
[ ] Functional requirements specified for each feature
[ ] Edge cases and error handling addressed

Non-Functional Requirements
[ ] Performance requirements specified (latency, throughput)
[ ] Security requirements documented
[ ] Usability/accessibility addressed
[ ] Scalability requirements defined
[ ] Compliance needs identified (if applicable)

User Stories / Use Cases
[ ] User stories follow standard format (As a... I want... So that...)
[ ] Acceptance criteria specified for each story
[ ] Multiple user types/personas considered if applicable

Success Criteria / Acceptance Criteria
[ ] Success criteria are measurable
[ ] Metrics have baselines and targets
[ ] Measurement method clearly specified
[ ] Realistic and achievable criteria

Timeline & Milestones
[ ] Key milestones identified (Discovery, Design, Dev, Launch)
[ ] Target dates are realistic
[ ] Dependencies between milestones considered
[ ] Ownership assigned for each milestone

Risks & Mitigation
[ ] Major risks identified
[ ] Impact and probability assessed for each risk
[ ] Mitigation strategies documented
[ ] Contingency plans in place for high-impact risks

Appendix
[ ] Supporting materials included (wireframes, API specs, etc.)
[ ] Related documents referenced
[ ] Research findings attached if applicable
```

**Quality Gates**:

**🟢 READY FOR REVIEW**:
- All 11 sections completed (at minimum with "TBD" placeholders)
- Executive summary clear
- Objectives measurable
- Key features documented

**🟡 IN REVIEW**:
- Feedback from stakeholders incorporated
- Technical feasibility confirmed
- Timeline validated with engineering
- Risks assessed and mitigated

**🔴 APPROVED**:
- All acceptance criteria finalized
- Timeline committed
- Resources allocated
- Ready for implementation

**Red Flags** (fix before proceeding):
- ❌ Vague success criteria ("improve user experience")
- ❌ Missing acceptance criteria for features
- ❌ Unrealistic timeline without buffer
- ❌ "Will discuss later" without concrete plan
- ❌ No risk mitigation for high-impact items
- ❌ Scope not clearly bounded

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

**Document Titles**:
```
PRD – [Product Name] – [Feature Title]
Product Requirements Document – [Feature Name]

Examples:
- PRD – Pegasus – Buy Again Model
- Product Requirements Document – Checkout Discount Code Feature
- PRD – Analytics – User Segmentation API
```

**File Names** (when saving locally):
```
output/prd-[team]-[product]-[feature]-[yyyymmdd].md

Examples:
- output/prd-ds-pegasus-buy-again-model-20260401.md
- output/prd-checkout-discount-code-20260315.md
- output/prd-analytics-user-segmentation-20260420.md
```

**Templates Location:**
- Reference template: `templates/prd-template.md`
- All templates stored in `/templates` folder

**Best Practice**: 
- Use clear, descriptive titles
- Include product/feature name
- Add version number if multiple iterations
- Always include date in filename for version tracking

---

## Template Customization

**Base Template**: Use `/templates/prd-template.md` as the starting point.

**When to Adapt**:

**For Standard Features**:
- Use template as-is with all 11 sections
- Focus on detailed functional requirements
- Include comprehensive acceptance criteria

**For Experiments/A/B Tests**:
- Add "Experiment Design" subsection under Key Features
- Include control vs treatment comparison
- Specify:
  - User segmentation method
  - Sample size & duration
  - Statistical significance threshold
  - Rollback plan

**For ML/Data Science Projects**:
- Expand Non-Functional Requirements with data requirements
- Add model specifications under Key Features
- Include:
  - Input features & data sources
  - Model architecture
  - Training/evaluation approach
  - Inference method (batch/real-time)
  - Model monitoring

**For Small Features/Quick Specs**:
- All 11 sections still required
- Can be brief but must be complete
- Use "TBD" for unknown items

**For Technical/Infrastructure Projects**:
- Emphasize Non-Functional Requirements
- Add API specifications in Appendix
- Include architecture diagrams
- Focus on security, scalability, performance

### Customization Guidelines:

✅ **DO**:
- Add subsections as needed for your project type
- Include relevant diagrams, mockups, flows
- Expand any section with project-specific details
- Reference related documents in Appendix

❌ **DON'T**:
- Skip any of the 11 core sections
- Remove acceptance criteria or success metrics
- Use vague language without specifics
- Omit timeline or risk assessment

---

## Integration with Other Tools

### Jira Integration

**Best Practices**:
- Reference Jira Epic in document header or Background section
- Use consistent naming between PRD and Epic
- Track implementation tasks in Jira
- Link tickets in Timeline & Milestones section

**Example Reference**:
```markdown
## 1. Document Title & Version
- **Product Name:** Checkout Discount Code
- **Jira Epic:** [DPT-123](https://finacceljira.atlassian.net/browse/DPT-123)
- **Document Version:** v1.0
- **Date:** 2026-04-06
- **Author:** Product Team
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
✅ All 11 sections completed (no missing sections)
✅ Clear product name, version, date, and author
✅ Concise executive summary (2-3 paragraphs)
✅ Specific, measurable objectives with business context
✅ Well-defined scope (In Scope & Out of Scope)
✅ Detailed feature descriptions with requirements
✅ Comprehensive non-functional requirements
✅ User stories with acceptance criteria
✅ Measurable success criteria with targets
✅ Realistic timeline with key milestones
✅ Identified risks with mitigation plans
✅ Supporting materials in appendix

**Common Issues to Avoid**:
❌ Vague requirements ("improve UX", "make it better")
❌ Success criteria without measurement method
❌ Missing user stories or acceptance criteria
❌ Unrealistic timeline without buffer
❌ No risk assessment
❌ Incomplete scope definition
❌ Missing non-functional requirements
❌ Poor formatting (inconsistent structure)
❌ Broken or missing references

**Review Checklist** (before finalizing):
1. All 11 sections present and complete
2. Stakeholders identified and aligned
3. Success metrics validated
4. Technical feasibility confirmed
5. Timeline agreed upon
6. Risks assessed and mitigated
7. Supporting documents linked

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

- **2026-04-06 v3.0**: Simplified to use standard `/templates/prd-template.md`
  - Removed complex Template v2 references
  - Aligned with 11-section standard template structure
  - Simplified validation checklist
  - Updated all examples to match template
  - Maintained flexibility for experiment and ML project variations
  
- **2026-04-02 v2.0**: Enhanced with comprehensive structure
  - Added detailed metadata fields
  - Enhanced Feature Requirements format
  - Added validation checklist and quality gates
  
- **2026-04-01 v1.0**: Initial version
