# Templates Folder

This folder contains **reference templates** for consistent output format across all generated content.

## Available Templates

### 📋 PRD Template (`prd-template.md`)
Complete Product Requirement Document structure with:
- Document metadata
- Executive summary
- Background & objectives
- Product scope
- Key features & functional requirements
- Non-functional requirements (performance, security, usability)
- User stories / use cases
- Success criteria / acceptance criteria
- Timeline & milestones
- Risks & mitigation
- Appendix

**Use for:** Creating comprehensive PRDs for new features, projects, or initiatives.

---

### 📝 Jira Templates

#### User Story Template (`jira-user-story-template.md`)
- Basic information (issue type, project, summary, priority, labels)
- User story format: "As a [persona], I want [capability], so that [value]"
- Background / context
- Acceptance criteria (Given-When-Then format)
- Technical details (API contract, data model)
- Design / mockups
- Testing requirements
- Definition of Done
- Story points estimate

**Use for:** Creating user stories for development work, feature requests, improvements.

---

#### Bug Template (`jira-bug-template.md`)
- Bug summary & impact
- Steps to reproduce
- Expected vs actual behavior
- Environment details (device, OS, browser, version)
- Screenshots / videos
- Logs / error messages
- Root cause analysis (to be filled by Engineering)
- Fix approach
- Acceptance criteria for fix
- Workaround (if available)
- Priority justification
- Definition of Done

**Use for:** Reporting bugs with complete context for quick resolution.

---

#### Epic Template (`jira-epic-template.md`)
- Epic overview & business problem
- Target users
- Success metrics (goal, metric, baseline, target)
- Scope (in scope / out of scope)
- User stories breakdown (must have, should have, could have)
- Dependencies
- Timeline & milestones
- Assumptions & validation plans
- Risks & mitigation
- Documentation links (PRD, design, tech spec)
- Stakeholders
- Definition of Done

**Use for:** Creating epics for large initiatives spanning multiple sprints.

---

#### Task Template (`jira-task-template.md`)
- Task overview & why it's needed
- Expected outcome
- Acceptance criteria
- Task breakdown (subtasks)
- Dependencies
- Technical details (files to change, code changes)
- Testing requirements
- Documentation updates
- Definition of Done
- Time estimate

**Use for:** Creating individual tasks for discrete pieces of work.

---

## How to Use Templates

### Via VS Code Copilot Chat

Simply ask:
```
Buatkan user story untuk fitur [nama fitur]
```

```
Generate bug ticket untuk issue [deskripsi]
```

```
Create PRD untuk [project name]
```

The agent will automatically:
1. Load the appropriate template
2. Fill in the sections based on context
3. Save the output to `/output` folder

### Manual Copy-Paste

1. Open the template file (e.g., `jira-user-story-template.md`)
2. Copy the content
3. Fill in the placeholders `[...]`
4. Paste into Jira

---

## Customization

Feel free to modify these templates to match your team's workflow:
- Add/remove sections
- Change field names
- Adjust acceptance criteria format
- Update definition of done checklist

---

**💡 Tip:** Keep templates up-to-date with your team's evolving standards and best practices.
