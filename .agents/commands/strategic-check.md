---
description: "Roadmap vs strategic priorities: OKR progress, priority drift detection, alignment scorecard"
argument-hint: "[priority-number]"
allowed-tools: ["Read", "Glob", "Grep", "Bash", "Agent"]
---

# Strategic Alignment Check

Assess progress against Liminal's 3 strategic priorities. Detect priority drift. Surface misaligned work.

**Focus:** $ARGUMENTS (1=Enterprise, 2=Agentic ROI, 3=Buyer App, blank=all)

## Instructions

You are the CPTO's chief-of-staff. Your job is to connect execution data to strategic intent and flag where they diverge.

### Step 0: Load Context

Read these files first:
- `.claude/product-context/strategic-goals.md` — The 3 strategic priorities and success metrics
- `.claude/product-context/current-roadmap.md` — Q1 initiatives mapped to priorities
- `.claude/product-context/team-info.md` — Team-to-priority mapping
- `.agents/skills/cpto-briefing/SKILL.md` — JQL templates, severity thresholds

### Step 1: Epic Status Pull

For each strategic priority (or just the specified one):

1. Query Jira for epics in LINK and DATA projects:
   - `jira_search` with JQL: `project = LINK AND type = Epic AND status != Done`
   - `jira_search` with JQL: `project = DATA AND type = Epic AND status != Done`
2. For each epic, note: key, summary, status, assignee, child issue count (if available)
3. Map epics to strategic priorities using `current-roadmap.md` initiative list

If Jira MCP is unavailable, use the roadmap file status as the best available data and note the gap.

### Step 2: Priority Drift Detection

Detect work that may not align with strategic priorities:

1. Query recently created tickets:
   - `project = LINK AND created >= -7d AND type not in (Sub-task, Epic) AND status != Done`
   - `project = DATA AND created >= -7d AND type not in (Sub-task, Epic) AND status != Done`
2. For each ticket, check if it has an Epic Link
3. Classify unlinked tickets:
   - **Aligned** — clearly related to a strategic priority based on summary/description
   - **Operational** — bugs, tech debt, infra (expected and healthy in moderation)
   - **Potentially drifting** — new feature work not connected to any priority

Calculate drift ratio: unlinked non-operational work / total recent work

### Step 3: Priority Scorecard

For each priority, produce:

```markdown
### Priority {N}: {Name} — {RED/YELLOW/GREEN}

**Owning Teams:** {team names}
**Key Initiatives:**

| Initiative | Team | Epic Key | Status | Progress | Risk |
|-----------|------|----------|--------|----------|------|

**Recent Activity (7 days):**
- {N} tickets created, {N} completed, {N} blocked
- Key deliverables this sprint: {list}

**Drift Detection:**
- Aligned work: {N} tickets ({%})
- Operational work: {N} tickets ({%})
- Potentially drifting: {N} tickets ({%}) — {list if any}

**So What:** {Interpretation — is this priority on track? What's the biggest risk?}
**Recommended Action:** {Specific action for the CPTO}
```

### Step 4: Overall Alignment Summary

```markdown
## Strategic Alignment Summary

| Priority | Status | On-Track Initiatives | At-Risk | Drift % |
|----------|--------|---------------------|---------|---------|

### Top Risks to Strategic Execution
1. {Biggest risk and why}
2. {Second risk}
3. {Third risk}

### Leadership Talking Points
- For next SLT meeting: {key point}
- For board context: {key point}
- For team all-hands: {key point}
```

### Step 5: Data Source Status

```markdown
---
**Data Sources:** Jira ({status}) | Roadmap file ({status}) | Strategic goals file ({status})
**Generated:** {current timestamp}
```
