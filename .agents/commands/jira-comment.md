---
description: Add a comment to a Jira ticket
---

Help add a well-formatted comment to a Jira issue.

## Arguments
$ARGUMENTS

## Process

1. **Get the issue key** - Parse from arguments or ask for ticket number (e.g., PROJ-123)
2. **Fetch current context** - Use `jira_get_issue` to understand the ticket
3. **Determine comment type** - Ask what kind of update they want to add
4. **Draft the comment** - Help format the comment appropriately
5. **Add the comment** - Use `jira_add_comment` to post it

## Comment Templates

### Status Update
```markdown
## Status Update - [Date]

**Progress**: [What was done]

**Next Steps**: [What's planned]

**Blockers**: [Any blockers, or "None"]

**ETA**: [If applicable]
```

### Question/Clarification
```markdown
@[person] - Question about this ticket:

[Clear question]

**Context**: [Why you're asking]
```

### Technical Note
```markdown
## Technical Note

[Technical details, findings, or implementation notes]

**Impact**: [What this affects]

**Action needed**: [If any]
```

### Resolution Summary
```markdown
## Resolution

**Root cause**: [What caused the issue]

**Fix**: [What was done to fix it]

**Verification**: [How it was tested]

**Related PRs**: [Links if applicable]
```

### Blocker/Dependency
```markdown
## Blocked

**Blocked by**: [Issue key or external dependency]

**Reason**: [Why this is blocking]

**Unblock criteria**: [What needs to happen]

**Workaround**: [If any temporary solution exists]
```

## Tips
- Use @mentions to notify specific people
- Keep comments focused on one topic
- Reference other tickets with [PROJ-123] format
- Use code blocks for technical content
- Include timestamps for time-sensitive updates
