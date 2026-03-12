---
description: Create comprehensive, detailed Jira tickets with full context and acceptance criteria
---

Create a high-quality, detailed Jira ticket by systematically gathering all necessary information.

## Arguments
$ARGUMENTS

## Goal
Create tickets that are:
- **Complete** - All necessary context included
- **Actionable** - Clear what needs to be done
- **Testable** - Specific acceptance criteria
- **Discoverable** - Proper labels and links

---

## Phase 1: Discovery

### 1.1 Get Projects
First, fetch available projects using `jira_get_all_projects` to show the user their options.

### 1.2 Gather Core Information
Ask the user (if not provided in arguments):

**Required:**
- What is the problem or goal? (Get detailed explanation)
- Which project? (Show project list)
- Issue type? (Bug, Story, Task, Spike, Epic)
- Priority? (Highest, High, Medium, Low, Lowest)

**Context Questions by Type:**

For **Bugs**:
- What is the expected behavior?
- What is the actual behavior?
- Steps to reproduce?
- Environment (browser, OS, device)?
- Error messages or logs?
- Screenshots or recordings available?
- Frequency (always, sometimes, rare)?
- Workaround available?

For **Stories/Features**:
- Who is the user/persona?
- What do they want to accomplish?
- Why is this valuable?
- How do they do this today?
- What does success look like?
- Any mockups or designs?
- Are there edge cases to consider?

For **Tasks**:
- What is the specific work to be done?
- What are the prerequisites?
- What systems/files are affected?
- Any dependencies on other work?

For **Spikes/Research**:
- What question are we trying to answer?
- What options should be evaluated?
- What are the decision criteria?
- Time-box duration?

---

## Phase 2: Research

### 2.1 Search for Related Issues
Use `jira_search` to find:

```
# Potential duplicates
text ~ "[key terms from description]" AND project = [PROJECT]

# Related work
labels = [relevant labels] AND project = [PROJECT]

# Recent similar issues
project = [PROJECT] AND created >= -30d AND text ~ "[keywords]"
```

Report findings:
- "Found X potentially related issues"
- List top 3-5 most relevant
- Ask if any are duplicates or should be linked

### 2.2 Check for Blockers
Ask: "Is this blocked by or does it block any other work?"

---

## Phase 3: Draft the Ticket

### Summary Format
`[Type Prefix] Clear, actionable description`

Prefixes by type:
- Bug: `[BUG]` or no prefix
- Feature: `Add`, `Implement`, `Enable`
- Task: `Update`, `Configure`, `Migrate`
- Spike: `[Spike]` or `[Research]`

Keep under 80 characters. Be specific.

### Description Templates

#### Bug Template
```markdown
## Summary
[One sentence describing the bug]

## Environment
- **Browser/App**: [e.g., Chrome 120, iOS app 2.3.1]
- **OS**: [e.g., macOS 14.2, Windows 11]
- **Environment**: [dev/staging/production]
- **User type**: [e.g., admin, regular user]

## Steps to Reproduce
1. [First step]
2. [Second step]
3. [Third step]

## Expected Behavior
[What should happen]

## Actual Behavior
[What actually happens]

## Error Details
```
[Error messages, stack traces, or logs if available]
```

## Screenshots/Recordings
[Attach or link to visual evidence]

## Frequency
- [ ] Always reproducible
- [ ] Intermittent (describe pattern)
- [ ] One-time occurrence

## Workaround
[If any temporary solution exists, describe it here]

## Impact
[Who is affected and how severely]

## Additional Context
[Any other relevant information]
```

#### Story/Feature Template
```markdown
## User Story
**As a** [type of user]
**I want** [goal/desire]
**So that** [benefit/value]

## Background
[Context and motivation for this feature]

## Detailed Requirements
[Comprehensive description of what needs to be built]

### Functional Requirements
1. [Requirement 1]
2. [Requirement 2]
3. [Requirement 3]

### User Flow
1. User starts at [starting point]
2. User takes action [action]
3. System responds with [response]
4. User sees [outcome]

## Acceptance Criteria
- [ ] **Given** [precondition], **when** [action], **then** [expected result]
- [ ] **Given** [precondition], **when** [action], **then** [expected result]
- [ ] **Given** [precondition], **when** [action], **then** [expected result]

## Edge Cases
| Scenario | Expected Behavior |
|----------|-------------------|
| [Edge case 1] | [How to handle] |
| [Edge case 2] | [How to handle] |

## Design/Mockups
[Links to Figma, screenshots, or design specs]

## Technical Notes
[Implementation hints, suggested approach, affected systems]

## Out of Scope
- [Explicitly list what this ticket does NOT cover]
- [This prevents scope creep]

## Dependencies
- [ ] [Dependency 1 - link to ticket if exists]
- [ ] [Dependency 2]

## Related Issues
- Related to: [PROJ-XXX]
- Blocks: [PROJ-YYY]
- Blocked by: [PROJ-ZZZ]

## Open Questions
- [ ] [Question that needs to be answered]
```

#### Task Template
```markdown
## Objective
[Clear statement of what needs to be accomplished]

## Background
[Why this task is needed]

## Scope of Work
### Include
- [Specific item 1]
- [Specific item 2]
- [Specific item 3]

### Exclude
- [What is NOT part of this task]

## Steps/Subtasks
- [ ] [Step 1]
- [ ] [Step 2]
- [ ] [Step 3]

## Acceptance Criteria
- [ ] [Criterion 1 - specific and measurable]
- [ ] [Criterion 2]
- [ ] [Criterion 3]

## Technical Details
[Relevant technical information, configurations, or specifications]

## Files/Systems Affected
- `path/to/file1`
- `path/to/file2`
- [System or service name]

## Testing Requirements
[How to verify this task is complete]

## Documentation
- [ ] Update [relevant documentation]
- [ ] No documentation changes needed

## Related Issues
[Links to related tickets]
```

#### Spike/Research Template
```markdown
## Research Question
[The specific question(s) we're trying to answer]

## Background
[Why we need this research, what problem it helps solve]

## Time Box
**Duration**: [X hours/days]
**Due**: [Date]

## Options to Evaluate
1. **Option A**: [Brief description]
2. **Option B**: [Brief description]
3. **Option C**: [Brief description]

## Evaluation Criteria
| Criteria | Weight | Notes |
|----------|--------|-------|
| [Criterion 1] | High/Med/Low | |
| [Criterion 2] | High/Med/Low | |
| [Criterion 3] | High/Med/Low | |

## Deliverables
- [ ] Summary document with findings
- [ ] Recommendation with rationale
- [ ] Proof of concept (if applicable)
- [ ] Follow-up tickets created

## Resources
- [Link to relevant documentation]
- [Link to similar implementations]

## Out of Scope
- [What this spike will NOT investigate]
```

---

## Phase 4: Review & Create

### 4.1 Show Complete Draft
Display the full ticket to the user:
- Project & Issue Type
- Summary
- Full Description
- Priority
- Labels (suggest appropriate ones)
- Assignee (if specified)
- Epic link (if applicable)
- Due date (if applicable)

### 4.2 Get Confirmation
Ask: "Does this look complete? Any changes before I create it?"

### 4.3 Create the Ticket
Use `jira_create_issue` with all gathered information.

### 4.4 Post-Creation Actions
After creating, offer to:
1. Link to an epic (`jira_link_to_epic`)
2. Link to related issues (`jira_create_issue_link`)
3. Create subtasks
4. Assign to someone
5. Add watchers

---

## Labels to Suggest

Based on content, suggest relevant labels:
- **Type**: `bug`, `feature`, `tech-debt`, `documentation`, `security`
- **Area**: `frontend`, `backend`, `api`, `database`, `infrastructure`, `mobile`
- **Team**: `[team-name]`
- **Priority**: `critical`, `quick-win`, `needs-design`, `needs-discussion`
- **Status**: `ready-for-dev`, `needs-refinement`, `blocked`
