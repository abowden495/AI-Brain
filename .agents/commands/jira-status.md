---
description: Change the status of a Jira ticket
---

Transition a Jira issue to a new status.

## Arguments
$ARGUMENTS

## Process

### Step 1: Get Issue Details
If an issue key is provided in arguments, fetch it with `jira_get_issue` to show:
- Current status
- Summary
- Assignee

If no issue key provided, ask the user for one.

### Step 2: Get Available Transitions
Use `jira_get_transitions` to fetch the valid status changes for this issue.

Display them clearly:
```
Current Status: In Progress

Available transitions:
1. Ready for Code Review
2. Blocked
3. Done
4. Won't Do
```

### Step 3: Transition the Issue
Once the user selects a status (by name or number), use `jira_transition_issue` to change it.

Optionally ask if they want to add a comment explaining the status change.

### Step 4: Confirm
Show the updated status and offer next actions:
- Add a comment
- View the updated ticket
- Transition another ticket

## Common Workflows

### Starting Work
```
/jira-status LINK-1234
> Select: "In Progress"
```

### Submitting for Review
```
/jira-status LINK-1234
> Select: "Ready for Code Review"
> Add comment: "PR: https://github.com/org/repo/pull/42"
```

### Closing a Ticket
```
/jira-status LINK-1234
> Select: "Done"
```

### Marking as Blocked
```
/jira-status LINK-1234
> Select: "Blocked"
> Add comment: "Waiting on API team to deploy auth changes"
```

## Tips
- Transition names vary by project workflow
- Some transitions may require fields (like resolution)
- If a transition fails, the tool will show available options
- You can type partial status names (e.g., "review" for "Ready for Code Review")
