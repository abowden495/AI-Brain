---
description: Show Jira tools and JQL syntax reference
---

Display a quick reference for Jira MCP tools and JQL query syntax.

## Available Jira Tools

### Reading Data
| Tool | Purpose |
|------|---------|
| `jira_get_issue` | Get full issue details including custom fields |
| `jira_search` | Search issues using JQL |
| `jira_get_all_projects` | List all accessible projects |
| `jira_get_project_issues` | Get issues for a specific project |
| `jira_get_transitions` | Get available status transitions |
| `jira_search_fields` | Search for field names |

### Agile/Sprints
| Tool | Purpose |
|------|---------|
| `jira_get_agile_boards` | List boards (scrum/kanban) |
| `jira_get_sprints_from_board` | Get sprints for a board |
| `jira_get_sprint_issues` | Get issues in a sprint |

### Creating & Updating
| Tool | Purpose |
|------|---------|
| `jira_create_issue` | Create a new ticket |
| `jira_update_issue` | Update issue fields |
| `jira_add_comment` | Add a comment |
| `jira_transition_issue` | Change status |

## JQL Quick Reference

```
# Basic filters
project = "PROJ"
assignee = currentUser()
status = "In Progress"
type = Bug

# Date filters
created >= -7d
updated >= startOfWeek()
duedate < now()

# Text search
text ~ "search term"
summary ~ "keyword"

# Combining conditions
project = PROJ AND status != Done
priority in (High, Highest) AND assignee is EMPTY

# Sorting
ORDER BY created DESC
ORDER BY priority ASC, created DESC
```

## Common Searches

| What you want | JQL |
|---------------|-----|
| My open tickets | `assignee = currentUser() AND status != Done` |
| Recent bugs | `project = PROJ AND type = Bug AND created >= -7d` |
| Sprint work | `sprint in openSprints() AND assignee = currentUser()` |
| Overdue | `duedate < now() AND status != Done` |
| Unassigned | `assignee is EMPTY AND status != Done` |

## Available Commands

| Command | Description |
|---------|-------------|
| `/jira-help` | This reference card |
| `/jira-search` | Search issues with natural language |
| `/jira-create` | Comprehensive guided ticket creation |
| `/jira-ticket` | Quick ticket creation |
| `/jira-status` | Change ticket status (transition) |
| `/jira-comment` | Add a formatted comment to a ticket |
