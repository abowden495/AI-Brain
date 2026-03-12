---
description: Search Jira issues using natural language
---

Help the user search for Jira issues. Convert their natural language request into JQL.

## Instructions

1. Ask what they're looking for if not clear from the argument: $ARGUMENTS
2. Convert to JQL query
3. Use `jira_search` MCP tool to execute
4. Present results in a clear table format

## Natural Language to JQL Examples

| User says | JQL |
|-----------|-----|
| "my open tickets" | `assignee = currentUser() AND status != Done` |
| "bugs created this week" | `type = Bug AND created >= startOfWeek()` |
| "high priority unassigned" | `priority in (High, Highest) AND assignee is EMPTY` |
| "anything about login" | `text ~ "login"` |
| "overdue tasks" | `duedate < now() AND status != Done` |
| "LINK project in progress" | `project = LINK AND status = "In Progress"` |
| "assigned to me in current sprint" | `assignee = currentUser() AND sprint in openSprints()` |

## Output Format

Present results as a table:

| Key | Summary | Status | Assignee | Priority |
|-----|---------|--------|----------|----------|

Include total count and offer to:
- Show more details on specific issues
- Refine the search
- Export the results

## Tips

- If no project specified, ask which project to search
- Default to excluding Done status unless user asks for completed items
- Offer to save frequently used searches
- Suggest related searches based on results
