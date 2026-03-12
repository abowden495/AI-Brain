---
description: "Full CPTO morning briefing: team health, product pulse, strategic alignment, and daily action plan"
argument-hint: "[quick]"
allowed-tools: ["Read", "Glob", "Grep", "Bash", "Agent"]
---

# CPTO Morning Briefing

Comprehensive daily briefing that surfaces execution risks, product health, and strategic alignment across all teams — with actionable recommendations for the day.

**Mode:** $ARGUMENTS (use "quick" for abbreviated version: blockers + alerts + top 3 actions only)

## Instructions

You are Andrew's chief-of-staff. Run a complete situational assessment and deliver it in a format optimized for a 5-minute read (or 90-second read in quick mode).

### Step 0: Load Context

Read ALL of these before starting:
- `.claude/product-context/team-info.md`
- `.claude/product-context/strategic-goals.md`
- `.claude/product-context/current-roadmap.md`
- `.claude/product-context/business-metrics.md`
- `.claude/product-context/current-features.md`
- `.agents/skills/cpto-briefing/SKILL.md`

### Quick Mode

If the argument is "quick", run an abbreviated version:
1. Pull only blocked items and high-priority alerts from Jira
2. Skip detailed sprint analysis, product metrics deep dive, and strategic alignment scoring
3. Jump straight to a `/my-day` style output with top 3 actions
4. Include a data source status footer
5. Offer to run the full briefing if anything looks concerning

### Full Mode (Default)

Run each section sequentially. Each section should be a complete analysis — not just raw data.

---

## Section 1: Executive Summary (write LAST, display FIRST)

After completing all sections, write the executive summary:

```markdown
# Morning Briefing — {date}

## 30-Second Read
| Dimension | Status | Headline |
|-----------|--------|----------|
| Team Execution | {RED/YELLOW/GREEN} | {one line} |
| Product Health | {RED/YELLOW/GREEN} | {one line} |
| Strategic Alignment | {RED/YELLOW/GREEN} | {one line} |

**Biggest risk today:** {one sentence}
**#1 action:** {one sentence}
**Good news:** {one sentence}

---
```

## Section 2: Team Health

Run the `/team-health` analysis:
- For each team (Core, App, Nexus, Data): sprint progress, blockers, stale tickets, risk level
- Cross-team summary table
- Who needs help today

Use the JQL templates from SKILL.md. For each team:
1. Find active sprint via board discovery
2. Query blocked, stale, and high-priority items
3. Calculate sprint completion percentage
4. Assign severity rating per the thresholds in SKILL.md

## Section 3: Product Pulse

Run the `/product-pulse` analysis:
- Query BigQuery for available engagement and adoption metrics
- Note Mixpanel/Sentry gaps with manual check URLs
- Feature adoption status for agentic capabilities
- Error health summary

If BigQuery is unavailable, note the gap and move on.

## Section 4: Strategic Alignment

Run the `/strategic-check` analysis:
- Epic status for each strategic priority
- Priority drift detection (unlinked recent work)
- Per-priority scorecard
- Leadership talking points

## Section 5: Your Day

Run the `/my-day` synthesis:
- Synthesize all findings from Sections 2-4
- Prioritized top 3 actions
- Unblock queue
- Recommended check-ins
- Watch list

---

## Footer

```markdown
---

## Data Source Status

| Source | Status | Notes |
|--------|--------|-------|
| Jira (LINK) | {connected/unavailable} | {details} |
| Jira (DATA) | {connected/unavailable} | {details} |
| BigQuery | {connected/unavailable} | {details} |
| Asana | {connected/unavailable} | {details} |
| MongoDB | {not queried} | Available if needed |
| Mixpanel | {manual check} | No MCP — check dashboard |
| Sentry | {manual check} | No MCP — check https://liminal-1m.sentry.io |

**Generated:** {timestamp}

---

**What's next?**
- "Drill into {section}" — get more detail on any area
- "Create tickets for action items" — turn recommendations into Jira tickets
- `/loop 24h /morning-briefing` — schedule this daily
```
