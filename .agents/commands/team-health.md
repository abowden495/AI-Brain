---
description: "Sprint execution across all teams: blockers, velocity, delivery risks, who needs help"
argument-hint: "[team-name]"
allowed-tools: ["Read", "Glob", "Grep", "Bash", "Agent"]
---

# Team Health Check

Surface sprint execution health across all engineering teams. Identify blockers, at-risk deliverables, and who needs help.

**Scope:** $ARGUMENTS (leave blank for all teams)

## Instructions

You are the CPTO's chief-of-staff. Read the skill knowledge base and team registry, then systematically check each team's sprint health.

### Step 0: Load Context

Read these files first:
- `.claude/product-context/team-info.md` — Team registry with Jira project keys, board info, leads
- `.agents/skills/cpto-briefing/SKILL.md` — JQL templates, severity thresholds, output formats
- `.claude/product-context/strategic-goals.md` — Strategic priorities (for context on what matters)

### Step 1: Discover Active Sprints

For each team in the registry (or just the specified team if an argument was given):

**Jira Teams (Core, App, Nexus — LINK project; Data — DATA project):**
1. Use `jira_get_agile_boards` to find boards for the project
2. Use `jira_get_sprints_from_board` with `state=active` to find the current sprint
3. Use `jira_get_sprint_issues` to get all issues in the active sprint

If Jira MCP is unavailable, clearly state this and skip to Asana.

### Step 2: Analyze Sprint Health (per team)

For each Jira team, run these JQL queries via `jira_search`:

1. **Blocked items:** `project = {KEY} AND status = "Blocked" AND sprint in openSprints()`
2. **Stale tickets (no update >3 days):** `project = {KEY} AND status = "In Progress" AND updated <= -3d`
3. **High priority unresolved:** `project = {KEY} AND priority in (High, Highest) AND status != Done AND sprint in openSprints()`
4. **Sprint completion:** Compare done vs total items in sprint
5. **Bug count:** `project = {KEY} AND type = Bug AND sprint in openSprints() AND status != Done`

### Step 3: Check Asana Bug Tracker

Query the Link Bug Tracker in Asana (project ID: `1200112298205290`):
- Use Asana MCP to get recent tasks, check for unresolved high-priority bugs
- Count open bugs by section/status

If Asana MCP is unavailable, note the gap and provide the manual URL.

### Step 4: Produce Report

For each team, output:

```markdown
### {Team Name} — {RED/YELLOW/GREEN}
**Sprint:** {sprint name} | **Progress:** {done}/{total} ({%}) | **Days remaining:** {N}
**PM:** {name} | **Eng Lead:** {name}

**Blockers ({count}):**
| Key | Summary | Assignee | Blocked Since |
|-----|---------|----------|---------------|

**At-Risk Items ({count}):**
- {Issue key}: {summary} — {why it's at risk}

**Stale Tickets ({count}):**
| Key | Summary | Assignee | Last Updated |
|-----|---------|----------|--------------|

**Bug Count:** {N} open in sprint

**So What:** {1-2 sentence interpretation — what does this mean for the CPTO?}
**Recommended Action:** {Specific: who to check in with, what to ask about}
```

### Step 5: Cross-Team Summary

After all teams, add:

```markdown
## Cross-Team Summary

| Team | Status | Sprint Progress | Blockers | Stale | Key Risk |
|------|--------|----------------|----------|-------|----------|

### Who Needs Help Today
1. {Most critical person/team and why}
2. {Second priority}
3. {Third priority}
```

### Step 6: Data Source Status

End with:
```markdown
---
**Data Sources:** Jira ({status}) | Asana ({status}) | BigQuery (not used) | Mixpanel (not used)
**Generated:** {current timestamp}
```
