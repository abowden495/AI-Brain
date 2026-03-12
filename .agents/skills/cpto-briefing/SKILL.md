---
name: cpto-briefing
description: Knowledge base for the CPTO morning briefing system. Contains metric definitions, JQL/SQL templates, output formats, severity thresholds, and degradation rules for team-health, product-pulse, strategic-check, my-day, and morning-briefing commands.
---

# CPTO Briefing System — Knowledge Base

## Data Source Mapping

### Available MCP Tools

| Data Need | MCP Tool | Parameters | Used By |
|-----------|----------|------------|---------|
| Sprint issues | `jira_get_sprint_issues` | `sprintId`, `fields` | /team-health |
| Search issues (JQL) | `jira_search` | `jql`, `fields`, `limit` | /team-health, /strategic-check |
| Agile boards | `jira_get_agile_boards` | — | /team-health (discover boards) |
| Board sprints | `jira_get_sprints_from_board` | `boardId` | /team-health (find active sprint) |
| Issue details | `jira_get_issue` | `issueKey` | /strategic-check (epic details) |
| Jira projects | `jira_get_all_projects` | — | /team-health (validation) |
| BigQuery SQL | `query` | `sql` | /product-pulse |
| Asana projects | `mcp__claude_ai_Asana__get_projects` | `team`, `limit` | /team-health |
| Asana tasks | `mcp__claude_ai_Asana__get_tasks` | `project`, `opt_fields` | /team-health |
| Asana search | `mcp__claude_ai_Asana__search_tasks_preview` | `query` | /team-health |

### Graceful Degradation

| Data Source | If Unavailable | Fallback Behavior |
|-------------|---------------|-------------------|
| Jira MCP | MCP server not connected | Show: "Jira MCP not available. Connect the Atlassian MCP server to enable sprint health tracking." |
| BigQuery MCP | MCP server not connected | Show: "BigQuery MCP not available. Connect @ergut/mcp-bigquery-server to enable product metrics." |
| Mixpanel | No MCP exists | Show: "Mixpanel metrics unavailable via MCP. Check dashboard manually: [dashboard URL]" |
| Sentry | No MCP exists | Show: "Error rates unavailable via MCP. Check Sentry: https://liminal-1m.sentry.io" |
| Asana MCP | MCP server not connected | Show: "Asana MCP not available. Check product board manually: [Asana URLs from team-info.md]" |
| MongoDB MCP | MCP server not connected | Show: "MongoDB not available. Connect MongoDB MCP to enable real-time app state queries." |

---

## JQL Templates

### Sprint Health Queries

```
# Active sprint issues for a board
# First: get boardId from jira_get_agile_boards
# Then: get active sprint from jira_get_sprints_from_board(boardId, state="active")
# Then: get issues from jira_get_sprint_issues(sprintId)

# Blocked items (any project)
project = {PROJECT_KEY} AND status = "Blocked" AND sprint in openSprints()

# Stale tickets (no update in 3+ days, still in progress)
project = {PROJECT_KEY} AND status = "In Progress" AND updated <= -3d

# Overloaded assignees (more than 5 open items)
project = {PROJECT_KEY} AND sprint in openSprints() AND status != Done AND assignee = "{assignee}"

# Items completed this sprint
project = {PROJECT_KEY} AND sprint in openSprints() AND status = Done

# Items remaining this sprint
project = {PROJECT_KEY} AND sprint in openSprints() AND status != Done

# High-priority unresolved
project = {PROJECT_KEY} AND priority in (High, Highest) AND status != Done AND sprint in openSprints()

# Bugs in current sprint
project = {PROJECT_KEY} AND type = Bug AND sprint in openSprints() AND status != Done

# Recently created (drift detection)
project = {PROJECT_KEY} AND created >= -7d AND type != Sub-task
```

### Strategic Check Queries

```
# Epic status for a project
project = {PROJECT_KEY} AND type = Epic AND status != Done

# Epic progress (count done vs total children)
"Epic Link" = {EPIC_KEY} AND status = Done
"Epic Link" = {EPIC_KEY}

# Work not linked to any epic (potential drift)
project = {PROJECT_KEY} AND "Epic Link" is EMPTY AND type not in (Sub-task, Epic) AND created >= -14d AND status != Done

# Cross-project priority alignment
project in (LINK, DATA) AND type = Epic AND status != Done ORDER BY priority DESC
```

---

## BigQuery SQL Templates

### Product Metrics

```sql
-- Daily Active Users (template — adjust table/column names after discovery)
SELECT
  DATE(activity_timestamp) as date,
  COUNT(DISTINCT user_id) as dau
FROM `{PROJECT}.{DATASET}.{USER_ACTIVITY_TABLE}`
WHERE DATE(activity_timestamp) >= DATE_SUB(CURRENT_DATE(), INTERVAL 30 DAY)
GROUP BY date
ORDER BY date DESC;

-- Weekly Active Users trend
SELECT
  DATE_TRUNC(DATE(activity_timestamp), WEEK) as week,
  COUNT(DISTINCT user_id) as wau
FROM `{PROJECT}.{DATASET}.{USER_ACTIVITY_TABLE}`
WHERE DATE(activity_timestamp) >= DATE_SUB(CURRENT_DATE(), INTERVAL 12 WEEK)
GROUP BY week
ORDER BY week DESC;

-- Feature adoption (template)
SELECT
  feature_name,
  COUNT(DISTINCT user_id) as unique_users,
  COUNT(*) as total_events
FROM `{PROJECT}.{DATASET}.{FEATURE_EVENTS_TABLE}`
WHERE DATE(event_timestamp) >= DATE_SUB(CURRENT_DATE(), INTERVAL 7 DAY)
GROUP BY feature_name
ORDER BY unique_users DESC;
```

> **Important:** These are templates. Run `/bq-explore` first to discover actual table names
> and schemas in the `analyticsdashboard-403720` GCP project, then update templates.

---

## Severity Classification

### Team Health Signals

| Severity | Criteria | Action |
|----------|----------|--------|
| RED | Any: blocked items >3 days, sprint completion <50% at midpoint, engineer with >8 open items, critical bug unresolved >2 days | Immediate intervention needed. CPTO should check in with team lead today. |
| YELLOW | Any: stale tickets (no update >3 days) >2, sprint completion tracking behind, bug count rising, team flagged concerns in retro | Monitor closely. Check in within 24 hours. |
| GREEN | Sprint on track, no blockers, bugs being resolved, team morale good | No action needed. Acknowledge good execution. |

### Product Health Signals

| Severity | Criteria | Action |
|----------|----------|--------|
| RED | WAU drop >15% W/W, error rate >5%, p95 latency >1000ms, critical feature broken | Escalate immediately. Align with VP Eng on response. |
| YELLOW | WAU flat for 2+ weeks, error rate 2-5%, new high-frequency Sentry errors, feature adoption <15% | Investigate root cause. Discuss in next product sync. |
| GREEN | Metrics stable or growing, error rates low, features being adopted | Healthy. Continue monitoring. |

### Strategic Alignment Signals

| Severity | Criteria | Action |
|----------|----------|--------|
| RED | >30% of recent work unlinked to strategic priorities, epic significantly behind schedule, key initiative blocked | Realign team focus. Discuss in leadership meeting. |
| YELLOW | 15-30% unlinked work, epic behind but recoverable, priority drift emerging | Flag in next planning session. |
| GREEN | <15% unlinked work, epics on track, teams aligned to priorities | Healthy alignment. |

---

## Output Format Standards

### Section Headers
Use consistent formatting across all commands:

```
## [ICON] Section Name
**Status:** RED / YELLOW / GREEN

[Content]
```

Icons:
- Team Health: use status indicators (critical/warning/ok)
- Product Metrics: use trend indicators (up/down/flat)
- Strategic: use alignment indicators (aligned/drifting/misaligned)

### Summary Tables
Always use markdown tables for scannable data:

```markdown
| Team | Sprint Progress | Blockers | Risk Level |
|------|----------------|----------|------------|
```

### Action Items
Always end sections with specific, actionable recommendations:

```markdown
### Recommended Actions
1. **[Priority]** [Specific action] — [who to talk to / what to do]
```

### Data Source Status
Every report should include a footer showing what data was available:

```markdown
---
**Data Sources:** Jira (connected) | BigQuery (connected) | Asana (connected) | Mixpanel (not available) | Sentry (not available)
**Generated:** {timestamp}
```

---

## Asana Integration Notes

Asana MCP is available and should be used for:
- Querying the Link Bug Tracker for bug counts and trends
- Checking product board task status
- Cross-functional project visibility

Key Asana project IDs (from team-info.md):
- Link Bug Tracker: `1200112298205290`
- Link Master Project Plan: `1204585924327174`
- Product and Engineering team: `1197478826768894`

### Asana MCP Tools Available

| Tool | Purpose |
|------|---------|
| `mcp__claude_ai_Asana__get_projects` | List projects by team |
| `mcp__claude_ai_Asana__get_tasks` | Get tasks in a project |
| `mcp__claude_ai_Asana__get_task` | Get single task details |
| `mcp__claude_ai_Asana__search_objects` | Search across workspace |
| `mcp__claude_ai_Asana__get_status_overview` | Get project status |

---

## Command Interdependencies

```
/morning-briefing
  ├── /team-health       (Jira + Asana data)
  ├── /product-pulse     (BigQuery + manual metrics)
  ├── /strategic-check   (Jira + strategic-goals.md + current-roadmap.md)
  └── /my-day            (synthesizes above 3 + calendar context)
```

Each command works standalone. When called from `/morning-briefing`, they receive context from prior commands to avoid redundant queries and enable cross-cutting insights.
