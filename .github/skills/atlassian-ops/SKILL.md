---
name: atlassian-ops
description: "Use when: interacting with Confluence and Jira via mcp-atlassian MCP — read/create/update pages, search Confluence spaces, manage Jira tickets, check sprint progress, write PRDs."
compatibility: vscode
metadata:
  tools: mcp-atlassian
  source: https://github.com/sooperset/mcp-atlassian
  workflow: product-management
license: MIT
---

# Atlassian Ops Skill

Powered by [sooperset/mcp-atlassian](https://github.com/sooperset/mcp-atlassian).

## What I do

- Search and read Confluence pages and spaces
- Create and update Confluence pages
- Add/reply to comments, manage labels and attachments on Confluence
- Search Jira tickets with JQL (by status, assignee, project, sprint)
- Get Jira issue details, transitions, watchers, worklogs
- Create and update Jira issues (single or batch)
- Transition Jira issue status (e.g. In Progress → Done)
- Manage sprints, versions, epics, and agile boards
- Access Jira Service Desk queues and SLA info

## How to use the MCP tools

Use the `mcp-atlassian` MCP server for all Atlassian operations.

### Confluence tools

| Tool | Description |
|------|-------------|
| `confluence_search` | Search pages with CQL |
| `confluence_get_page` | Get full page content |
| `confluence_create_page` | Create a new page |
| `confluence_update_page` | Update existing page content |
| `confluence_get_page_children` | List child pages |
| `confluence_get_page_history` | Get page revision history |
| `confluence_get_page_diff` | Diff between page versions |
| `confluence_get_page_views` | Get page view stats |
| `confluence_get_comments` | Get comments on a page |
| `confluence_add_comment` | Add a comment to a page |
| `confluence_reply_to_comment` | Reply to an existing comment |
| `confluence_get_labels` | Get labels on a page |
| `confluence_add_label` | Add a label to a page |
| `confluence_get_attachments` | List attachments on a page |
| `confluence_upload_attachment` | Upload a single attachment |
| `confluence_upload_attachments` | Upload multiple attachments |
| `confluence_download_attachment` | Download an attachment |
| `confluence_download_content_attachments` | Download all attachments from a page |
| `confluence_get_page_images` | Get images embedded in a page |
| `confluence_move_page` | Move a page to a different parent/space |
| `confluence_search_user` | Search for Confluence users |

### Jira tools

| Tool | Description |
|------|-------------|
| `jira_search` | Search issues with JQL |
| `jira_get_issue` | Get full issue details |
| `jira_create_issue` | Create a new issue |
| `jira_update_issue` | Update issue fields |
| `jira_transition_issue` | Change issue status |
| `jira_get_transitions` | List available transitions for an issue |
| `jira_batch_create_issues` | Create multiple issues at once |
| `jira_batch_get_changelogs` | Get changelogs for multiple issues |
| `jira_add_comment` | Add a comment to an issue |
| `jira_edit_comment` | Edit an existing comment |
| `jira_get_worklog` | Get worklogs for an issue |
| `jira_add_worklog` | Log time to an issue |
| `jira_add_watcher` | Add a watcher to an issue |
| `jira_remove_watcher` | Remove a watcher |
| `jira_get_issue_watchers` | List watchers |
| `jira_get_issue_dates` | Get start/due dates |
| `jira_get_issue_development_info` | Get linked PRs, branches, commits |
| `jira_get_issues_development_info` | Batch version of above |
| `jira_get_issue_images` | Get images attached to an issue |
| `jira_get_issue_sla` | Get SLA status (Service Desk) |
| `jira_get_issue_proforma_forms` | Get ProForma form data |
| `jira_update_proforma_form_answers` | Update ProForma form answers |
| `jira_get_proforma_form_details` | Get ProForma form schema |
| `jira_download_attachments` | Download attachments from an issue |
| `jira_get_all_projects` | List all Jira projects |
| `jira_get_project_issues` | Get all issues in a project |
| `jira_get_project_components` | List project components |
| `jira_get_project_versions` | List project versions/releases |
| `jira_create_version` | Create a new version |
| `jira_batch_create_versions` | Create multiple versions |
| `jira_get_field_options` | Get field picklist options |
| `jira_search_fields` | Search available Jira fields |
| `jira_get_link_types` | List issue link types |
| `jira_create_issue_link` | Link two issues together |
| `jira_create_remote_issue_link` | Add a remote (URL) link to an issue |
| `jira_remove_issue_link` | Remove a link between issues |
| `jira_link_to_epic` | Link an issue to an epic |
| `jira_get_agile_boards` | List all agile boards |
| `jira_get_board_issues` | Get issues on a board |
| `jira_get_sprints_from_board` | List sprints for a board |
| `jira_get_sprint_issues` | Get issues in a sprint |
| `jira_create_sprint` | Create a new sprint |
| `jira_update_sprint` | Update sprint details |
| `jira_add_issues_to_sprint` | Add issues to a sprint |
| `jira_get_user_profile` | Get a user's profile info |
| `jira_get_service_desk_for_project` | Get Service Desk for a project |
| `jira_get_service_desk_queues` | List Service Desk queues |
| `jira_get_queue_issues` | Get issues in a queue |

## Story Points (customfield_10027)

MCP `jira_search` / `jira_get_issue` **tidak** mengekspos nilai custom field di response-nya. Untuk membaca Story Points, gunakan **Jira REST API v3** langsung.

> ⚠️ Jira REST API v2 (`/rest/api/2/search`) sudah di-remove. Selalu gunakan v3.

### Field mapping

| Custom Field ID | Nama | Tipe |
|---|---|---|
| `customfield_10027` | Story Points | Number (float) |

### Command template (curl + python)

```bash
curl -s -u "$JIRA_USERNAME:$JIRA_API_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d '{"jql":"project=DPT AND sprint in openSprints()","fields":["summary","status","assignee","customfield_10027"],"maxResults":50}' \
  "https://finacceljira.atlassian.net/rest/api/3/search/jql" \
  | python3 -c "
import json, sys
data = json.load(sys.stdin)
issues = data.get('issues', [])
sp_by_status = {}
for i in issues:
    sp = i['fields'].get('customfield_10027') or 0
    status = i['fields']['status']['name']
    sp_by_status[status] = sp_by_status.get(status, 0) + sp
print('SP per status:', json.dumps(sp_by_status, indent=2))
print('Total SP:', sum(sp_by_status.values()))
"
```

### JQL patterns

```
# Sprint aktif
project = DPT AND sprint in openSprints()

# Filter tiket yang punya SP
project = DPT AND sprint in openSprints() AND "Story Points" is not EMPTY

# Filter by SP minimum
project = DPT AND sprint in openSprints() AND cf[10027] >= 3
```

### Kredensial (dari .vscode/mcp.json)

- **URL**: `https://finacceljira.atlassian.net`
- **Username**: `rushan.faizal@finaccel.co`
- **Token**: gunakan `JIRA_API_TOKEN` dari `.vscode/mcp.json`

## Example prompts

- "Cek tiket Jira yang statusnya In Progress di project PROJ"
- "Update halaman PRD di Confluence space 'Product' dengan section baru"
- "Buat halaman baru di Confluence space 'Engineering' dengan judul 'API Design v2'"
- "Cari semua tiket Jira yang assigned ke saya"
- "Transition tiket PROJ-123 ke status Done"
- "Buatkan ringkasan sprint saat ini — apa yang sudah done, apa yang blocked?"
- "Cari halaman Confluence tentang [nama fitur]"
- "Generate release notes berdasarkan tiket yang selesai di sprint ini"
- "Batch create tiket untuk semua user story di sprint berikutnya"
- "Lihat development info (PR, branch) untuk tiket FEAT-456"
- "Cek SLA status untuk semua open tiket di Service Desk queue"

## When to use me

Use this skill when the user wants to:
- Check, create, or update Jira tickets/issues
- Read, write, or update Confluence pages or PRDs
- Search Atlassian content
- Manage project documentation
- Summarize sprint progress or generate reports
- Manage sprints, boards, epics, versions
- Access Service Desk queues and SLA data

## Notes

- Credentials dikonfigurasi di `.vscode/mcp.json` di workspace ini — menggunakan `uvx mcp-atlassian` (sooperset)
- Jika ada auth error, verifikasi `CONFLUENCE_API_TOKEN` dan `JIRA_API_TOKEN` sudah benar
- API token bisa dibuat di: https://id.atlassian.com/manage-profile/security/api-tokens
- Untuk Jira Cloud: gunakan `JIRA_URL` + `JIRA_USERNAME` + `JIRA_API_TOKEN`
- Untuk Jira Server/DC: set `JIRA_PERSONAL_TOKEN` sebagai ganti username+token
