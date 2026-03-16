# Copilot PM Toolkit

A GitHub Copilot customization toolkit for Product Managers — powered by **MCP (Model Context Protocol)** integration with Jira and Confluence.

With this toolkit, GitHub Copilot acts as your **Senior PM assistant** capable of:
- Reading & creating Jira tickets, managing sprints, checking backlog
- Reading & writing Confluence pages, PRDs, meeting notes
- Drafting PRDs with structured format (Objective, Success Metrics, User Stories, Constraints)
- Identifying risks and blockers from sprint data

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
│       └── atlassian-ops/
│           └── SKILL.md               # Full Jira + Confluence tool reference (67+ tools)
└── .vscode/
    ├── mcp.json                        # Your credentials (gitignored, not in repo)
    ├── mcp.json.example                # Template — copy this and fill your creds
    └── settings.json                   # VS Code config
```

### Jira Tools (examples)
- `jira_search` — query issues with JQL
- `jira_get_issue` — get full ticket details
- `jira_create_issue` / `jira_update_issue` — create or update tickets
- `jira_transition_issue` — move ticket between statuses
- `jira_get_sprint_issues` — list all issues in a sprint
- `jira_get_sprints_from_board` — view sprint history & active sprint

### Confluence Tools (examples)
- `confluence_search` — full-text search across spaces
- `confluence_get_page` / `confluence_create_page` / `confluence_update_page`
- `confluence_add_comment` — comment on pages
- `confluence_get_page_history` — track changes

Full list in [.github/skills/atlassian-ops/SKILL.md](.github/skills/atlassian-ops/SKILL.md).

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
