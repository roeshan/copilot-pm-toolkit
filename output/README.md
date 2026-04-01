# Output Folder

This folder contains **all generated content** from the PM Toolkit agent:

- **PRD Drafts** — Product Requirement Documents
- **Ticket Drafts** — Jira tickets (User Stories, Bugs, Epics, Tasks)
- **Analysis Reports** — Sprint analysis, backlog reports, metrics analysis
- **Sprint Reports** — Sprint summaries, velocity tracking

## Naming Convention

All files follow this format:
```
[type]-[name/topic]-[YYYYMMDD].md
```

Examples:
- `prd-slack-bot-senior-pm-agent-20260402.md`
- `ticket-user-story-checkout-discount-20260402.md`
- `analysis-sprint-velocity-Q1-20260402.md`
- `report-sprint-25-retrospective-20260402.md`

## Safety Notes

- ⚠️ This folder is in `.gitignore` — files here are NOT committed to Git
- 💾 Back up important files if needed
- 🗑️ Safe to delete old drafts — they won't affect the toolkit

## File Types

### PRD Drafts (`prd-*.md`)
Complete Product Requirement Documents with:
- Metadata (owners, reviewers, timeline)
- Objective & problem statement
- Success metrics
- Requirements & acceptance criteria
- API contracts

### Ticket Drafts (`ticket-*.md`)
Jira ticket descriptions ready to copy-paste:
- User stories with acceptance criteria
- Bug reports with reproduction steps
- Epics with milestones
- Tasks with checklists

### Analysis Reports (`analysis-*.md`)
Data-driven insights:
- Sprint velocity trends
- Backlog health checks
- Blocker analysis
- Story points distribution

### Sprint Reports (`sprint-*.md`)
Sprint summaries:
- Completed vs planned work
- Velocity tracking
- Team capacity analysis
- Retrospective notes

---

**💡 Tip:** Reference the `/templates` folder for consistent formatting across all outputs.
