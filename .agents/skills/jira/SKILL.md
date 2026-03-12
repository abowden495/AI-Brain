---
name: jira
description: Provides Jira expertise for searching issues, creating detailed tickets, adding comments, and managing workflows. Use this skill when the user asks about Jira tickets, needs to create issues, wants to search for tickets, or needs help with JQL queries. Emphasizes creating comprehensive, well-documented tickets.
---

# Jira Assistant

This skill leverages the Atlassian MCP server for Jira operations with a focus on creating high-quality, detailed tickets.

## Philosophy: Great Tickets

A great ticket is:
- **Complete** - Contains all context needed to understand and implement
- **Actionable** - Clear what needs to be done
- **Testable** - Has specific acceptance criteria
- **Discoverable** - Properly labeled and linked

## Available Commands

| Command | Purpose |
|---------|---------|
| `/jira-create` | **Comprehensive ticket creation** - guides through gathering all details |
| `/jira-search` | Search issues with natural language |
| `/jira-comment` | Add formatted comments |
| `/jira-help` | Quick reference card |

## Available MCP Tools

### Reading Data
| Tool | Purpose |
|------|---------|
| `jira_get_issue` | Get full issue details including custom fields |
| `jira_search` | Search issues using JQL |
| `jira_get_all_projects` | List all accessible projects |
| `jira_get_project_issues` | Get issues for a specific project |
| `jira_get_transitions` | Get available status transitions |
| `jira_search_fields` | Search for custom field names |

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
| `jira_add_comment` | Add a comment to an issue |
| `jira_transition_issue` | Change issue status |

### Linking
| Tool | Purpose |
|------|---------|
| `jira_link_to_epic` | Link an issue to an epic |
| `jira_create_issue_link` | Link two issues |

---

## Ticket Creation Workflow

When the user wants to create a ticket:

### 1. Discovery Phase
- Get available projects with `jira_get_all_projects`
- Ask clarifying questions based on issue type
- For bugs: reproduction steps, environment, expected vs actual
- For features: user story, acceptance criteria, edge cases
- For tasks: scope, steps, affected systems

### 2. Research Phase
- Search for duplicates with `jira_search`
- Find related issues
- Identify potential blockers or dependencies

### 3. Draft Phase
- Construct comprehensive description using templates
- Include acceptance criteria (Given/When/Then format)
- Add technical notes and out-of-scope section
- Suggest appropriate labels

### 4. Create Phase
- Show complete draft for review
- Create with `jira_create_issue`
- Offer to link to epics and related issues

---

## Description Templates

### Bug Template
```markdown
## Summary
[One sentence describing the bug]

## Environment
- **Browser/App**:
- **OS**:
- **Environment**: [dev/staging/production]

## Steps to Reproduce
1.
2.
3.

## Expected Behavior
[What should happen]

## Actual Behavior
[What actually happens]

## Acceptance Criteria
- [ ] Bug no longer reproducible following steps above
- [ ] Regression test added
- [ ] No side effects in related functionality
```

### Feature/Story Template
```markdown
## User Story
**As a** [user type]
**I want** [goal]
**So that** [benefit]

## Background
[Context and motivation]

## Acceptance Criteria
- [ ] **Given** [precondition], **when** [action], **then** [result]
- [ ] **Given** [precondition], **when** [action], **then** [result]

## Edge Cases
| Scenario | Expected Behavior |
|----------|-------------------|
| | |

## Technical Notes
[Implementation hints]

## Out of Scope
- [What this does NOT include]
```

### Task Template
```markdown
## Objective
[Clear goal]

## Scope
### Include
-

### Exclude
-

## Acceptance Criteria
- [ ]
- [ ]

## Files/Systems Affected
-
```

---

## JQL Quick Reference

```
# My open work
assignee = currentUser() AND status != Done

# Project bugs
project = PROJ AND type = Bug AND status != Done

# Current sprint
sprint in openSprints()

# Recently updated
updated >= -1d

# Text search
text ~ "search terms"

# Overdue
duedate < now() AND status != Done
```

---

## Best Practices

### Summaries
- Start with action verb: Add, Fix, Update, Implement
- Be specific: "Fix login timeout on mobile" not "Login broken"
- Under 80 characters

### Acceptance Criteria
- Use Given/When/Then format
- Make them testable and specific
- Include edge cases

### Labels
Use consistent labels for discoverability:
- Type: `bug`, `feature`, `tech-debt`
- Area: `frontend`, `backend`, `api`
- Status: `ready-for-dev`, `needs-discussion`

### Links
- Always search for related issues before creating
- Link duplicates with "is duplicated by"
- Link dependencies with "blocks" / "is blocked by"
- Link to parent epics
