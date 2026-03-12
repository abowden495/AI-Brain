---
description: "Product metrics: adoption, engagement, funnel health, error rates"
argument-hint: "[metric-category]"
allowed-tools: ["Read", "Glob", "Grep", "Bash", "Agent"]
---

# Product Pulse

Surface product health metrics: user engagement, feature adoption, error rates, and funnel health.

**Focus:** $ARGUMENTS (engagement, agentic, errors, all — default: all)

## Instructions

You are the CPTO's chief-of-staff analyzing product health signals. Focus on what's changed, what's trending, and what needs attention.

### Step 0: Load Context

Read these files first:
- `.claude/product-context/business-metrics.md` — Metric definitions, data sources, thresholds
- `.claude/product-context/current-features.md` — Active features with tracking events
- `.agents/skills/cpto-briefing/SKILL.md` — SQL templates, severity thresholds, degradation rules

### Step 1: Check Data Source Availability

Before querying, verify which MCP tools are available:
- Try a simple BigQuery query (e.g., `SELECT 1`) to confirm connectivity
- Note which sources are available vs unavailable

### Step 2: Query Available Metrics

**If BigQuery is available:**

1. **Discover tables first** (if not yet mapped in business-metrics.md):
   ```sql
   SELECT schema_name FROM INFORMATION_SCHEMA.SCHEMATA
   ```
   Then explore relevant datasets for user activity and event tables.

2. **Engagement metrics** (using templates from SKILL.md, adjusted for actual table names):
   - DAU / WAU / MAU trends (last 4 weeks)
   - Session counts and trends
   - Active account counts

3. **Feature adoption** (if event tables found):
   - Usage by feature (last 7 days vs prior 7 days)
   - New feature activation rates
   - Agentic feature usage (Scout Agent, Insights Agent, Coach AI, Team Spaces)

4. **Data pipeline health** (if applicable):
   - Event processing volumes
   - Data freshness indicators

**If BigQuery is unavailable:**
Note the gap and recommend connecting the BigQuery MCP server.

### Step 3: Check Error Health

**Sentry (manual check needed):**
- Note that error rates require manual check at https://liminal-1m.sentry.io
- Reference any known high-frequency errors from recent retros (Core team flagged recurring Sentry errors)

**Feature flags (manual check needed):**
- Note active flags at https://features.liminal-infra.com

### Step 4: Produce Report

```markdown
## Product Pulse — {date}

### Overall Health: {RED/YELLOW/GREEN}

### Engagement Dashboard

| Metric | Current | Prior Period | Trend | Status |
|--------|---------|-------------|-------|--------|
| DAU | {N} | {N} | {up/down/flat} | {status} |
| WAU | {N} | {N} | {up/down/flat} | {status} |
| MAU | {N} | {N} | {up/down/flat} | {status} |
| Active Accounts | {N} | {N} | {up/down/flat} | {status} |

### Feature Adoption

| Feature | Users (7d) | Change vs Prior 7d | Adoption Rate | Status |
|---------|-----------|-------------------|---------------|--------|

### Agentic Capabilities

| Capability | Accounts Using | Sessions/Queries (7d) | Trend | Status |
|-----------|---------------|----------------------|-------|--------|
| Coach AI | {N} | {N} | {trend} | {status} |
| Insights Agent | {N} | {N} | {trend} | {status} |
| Scout Agent / TALs | {N} | {N} | {trend} | {status} |
| Team Spaces | {N} | {N} | {trend} | {status} |

### Error Health
- **Frontend error rate:** {check Sentry manually}
- **Backend error rate:** {check Sentry manually}
- **High-frequency errors:** {reference from retros if known}

### So What
{2-3 sentence interpretation of overall product health. What's the headline?}

### Recommended Actions
1. {Most important product action}
2. {Second action}
3. {Third action}

### Manual Checks Needed
- [ ] Sentry dashboard: https://liminal-1m.sentry.io
- [ ] Mixpanel dashboard: {URL if known}
- [ ] Feature flags: https://features.liminal-infra.com
```

### Step 5: Data Source Status

```markdown
---
**Data Sources:** BigQuery ({status}) | Sentry (manual) | Mixpanel (manual) | Unleash (manual)
**Generated:** {current timestamp}
```
