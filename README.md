# Copilot PM Toolkit

A GitHub Copilot customization toolkit for Product Managers — powered by **MCP (Model Context Protocol)** integration with Jira and Confluence.

> 🔒 **Default Configuration: READ-ONLY MODE**  
> This toolkit is configured for **safe exploration** with search & read permissions only.  
> Write operations (create/update/delete) are disabled by default to prevent accidental modifications.

With this toolkit, GitHub Copilot acts as your **Senior PM assistant** capable of:
- ✅ **Search & analyze** Jira tickets, sprint progress, roadmap data
- ✅ **Search & read** Confluence pages, PRDs, meeting notes, documentation  
- ✅ **Generate insights** from backlog, identify blockers, analyze metrics
- ✅ **Draft PRDs locally** with structured format (Objective, Success Metrics, AC)
- ❌ **No accidental modifications** — create/update operations disabled by default

---

## Prerequisites

| Tool | Version | Notes |
|------|---------|-------|
| [VS Code](https://code.visualstudio.com/) | Latest | + GitHub Copilot extension |
| [GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat) | Latest | Copilot Chat required |
| [uv / uvx](https://docs.astral.sh/uv/getting-started/installation/) | Latest | To run `mcp-atlassian` |
| Atlassian API Token | — | See step 2 below |

---

## Setup

### 1. Clone the repo

```bash
git clone https://github.com/roeshan/copilot-pm-toolkit.git
cd copilot-pm-toolkit
```

### 2. Generate your Atlassian API Token

1. Go to: **https://id.atlassian.com/manage-profile/security/api-tokens**
2. Click **Create API token**
3. Label it something like `copilot-pm-toolkit`
4. Copy the token — you'll only see it once

### 3. Configure MCP credentials

Copy the example config and fill in your details:

```bash
cp .vscode/mcp.json.example .vscode/mcp.json
```

Then open `.vscode/mcp.json` and replace the placeholders:

```json
{
  "servers": {
    "mcp-atlassian": {
      "command": "uvx",
      "args": ["mcp-atlassian"],
      "env": {
        "CONFLUENCE_URL": "https://YOUR_DOMAIN.atlassian.net/wiki",
        "CONFLUENCE_USERNAME": "your-email@company.com",
        "CONFLUENCE_API_TOKEN": "YOUR_ATLASSIAN_API_TOKEN",
        "JIRA_URL": "https://YOUR_DOMAIN.atlassian.net",
        "JIRA_USERNAME": "your-email@company.com",
        "JIRA_API_TOKEN": "YOUR_ATLASSIAN_API_TOKEN"
      }
    }
  }
}
```

> ⚠️ `.vscode/mcp.json` is in `.gitignore` — your credentials will never be pushed to GitHub.

### 4. Install uvx (if not already installed)

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Or via Homebrew:
```bash
brew install uv
```

### 5. Open in VS Code & start chatting

Open the folder in VS Code, open Copilot Chat (`Cmd+Shift+I`), and try:

```
Tampilkan sprint aktif di board kita
```

```
Buatkan PRD untuk fitur [nama fitur]
```

```
Cari semua tiket dengan status In Progress di project PM
```

---

## What's Included

```
.
├── .github/
│   ├── instructions/
│   │   └── senior-pm.instructions.md   # PM persona & guidelines for Copilot
│   └── skills/
│       ├── atlassian-ops/
│       │   └── SKILL.md                # Full Jira + Confluence tool reference (67+ tools)
│       └── prd-writer/
│           └── SKILL.md                # PRD generation workflow
├── .vscode/
│   ├── mcp.json                        # Your credentials (gitignored, not in repo)
│   ├── mcp.json.example                # Template — copy this and fill your creds
│   └── settings.json                   # VS Code config + tool restrictions (READ-ONLY mode)
└── 11-prd-template.md                  # PRD template structure
```

---

## 🔒 Read-Only Mode (Default)

By default, this toolkit is configured for **safe exploration** to prevent accidental modifications:

### ✅ Allowed Operations
- Search Jira issues with JQL
- Get issue details, comments, history
- Search Confluence pages
- Read PRDs, documentation, meeting notes
- Analyze sprint progress & metrics
- Generate local drafts (PRDs, reports)

### ❌ Prohibited Operations  
- Create/update/delete Jira tickets
- Transition issue status
- Create/update Confluence pages
- Add comments or labels
- Upload attachments

**Configuration:** Write operations are disabled via `.vscode/settings.json` → `github.copilot.chat.tools.disabled`

**Enable Write Mode:** Edit `.vscode/settings.json` and remove specific tools from the disabled list. Restart VS Code after changes.

---

## Available MCP Tools

### Jira Tools (Read-Only by Default)
- ✅ `jira_search` — query issues with JQL
- ✅ `jira_get_issue` — get full ticket details
- ✅ `jira_get_sprint_issues` — list all issues in a sprint
- ✅ `jira_get_sprints_from_board` — view sprint history & active sprint
- ❌ `jira_create_issue` / `jira_update_issue` — **DISABLED**
- ❌ `jira_transition_issue` — **DISABLED**

### Confluence Tools (Read-Only by Default)
- ✅ `confluence_search` — full-text search across spaces
- ✅ `confluence_get_page` — read page content
- ✅ `confluence_get_page_history` — track changes
- ❌ `confluence_create_page` / `confluence_update_page` — **DISABLED**
- ❌ `confluence_add_comment` — **DISABLED**

Full list (67+ tools) in [.github/skills/atlassian-ops/SKILL.md](.github/skills/atlassian-ops/SKILL.md).

---

## Usage Examples (Read-Only Mode)

### Sprint Analysis
```
Analisa sprint aktif di board DPT — berapa tiket done vs in progress?
```

### Search PRDs
```
Cari PRD tentang "recommendation engine" di space DS
```

### Identify Blockers
```
List semua tiket yang stuck lebih dari 5 hari tanpa update di project DPT
```

### Story Points Aggregation
```
Hitung total Story Points di sprint aktif per status (To Do, In Progress, Done)
```

### Generate Local Drafts
```
Bikin draft PRD untuk "User Segmentation v3" dan simpan di local file
```

Ask Copilot for more examples tailored to your workflow.

---

## Security Notes

- **Never commit `.vscode/mcp.json`** — it contains your personal API token
- Each PM uses their own token — do not share tokens between team members
- If your token is accidentally exposed, revoke it immediately at https://id.atlassian.com/manage-profile/security/api-tokens

---

## Contributing

PRs welcome for:
- New skill files (e.g., `linear-ops`, `notion-ops`)
- Additional PM instruction templates
- Improved PRD structures or prompt examples
