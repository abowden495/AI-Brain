---
description: Create a detailed, well-structured Jira ticket
---

Help create a comprehensive Jira ticket by gathering requirements and context.

## Arguments
$ARGUMENTS

## Process

### Step 1: Gather Information
If not provided in the arguments, ask the user about:
- What problem needs to be solved or feature needed?
- Which project should this be in? (use `jira_get_all_projects` to list options)
- What type of issue? (Bug, Story, Task, Epic)
- Priority level?
- Any specific acceptance criteria?
- Who should be assigned?

### Step 2: Search for Related Issues
Use `jira_search` to find:
- Potential duplicates (search by keywords)
- Related existing work
- Similar past issues

Report findings to user before proceeding.

### Step 3: Draft the Ticket
Create a well-structured ticket with:

**Summary**: Clear, actionable, under 80 chars
- Good: "Add password reset flow to mobile app"
- Bad: "Password issue"

**Description** (use this template):
```markdown
## Problem/Goal
[Clear statement of what and why]

## Acceptance Criteria
- [ ] Specific, testable criterion 1
- [ ] Specific, testable criterion 2
- [ ] Specific, testable criterion 3

## Technical Notes
[Implementation hints, affected systems, dependencies]

## Out of Scope
[Explicitly state what this does NOT include]

## Related Issues
[Links to related tickets found in search]
```

### Step 4: Confirm and Create
Show the user the complete draft including:
- Project key
- Issue type
- Summary
- Full description
- Priority
- Labels (if any)
- Assignee (if any)

Ask for confirmation, then create with `jira_create_issue`.

### Step 5: Post-Creation
After creating:
- Show the new ticket key and link
- Offer to link to an epic if appropriate
- Offer to create related sub-tasks
- Ask if they want to create another ticket

## Tips
- For bugs: Always include reproduction steps in description
- For features: Include user story format if appropriate ("As a... I want... So that...")
- Add appropriate labels for discoverability
- Set realistic priority based on impact
- Link to relevant documentation or designs if mentioned
