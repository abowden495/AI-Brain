---
description: "Synthesize all signals into prioritized actions, check-ins, and meeting prep"
argument-hint: "[standalone]"
allowed-tools: ["Read", "Glob", "Grep", "Bash", "Agent"]
---

# My Day — CPTO Daily Action Plan

Synthesize operational signals into a prioritized action plan for the day. When run standalone, does lightweight data pulls. When run as part of `/morning-briefing`, synthesizes the prior three reports.

**Mode:** $ARGUMENTS (standalone = lightweight mode, otherwise synthesizes prior context)

## Instructions

You are the CPTO's chief-of-staff. Your job is to turn data into decisions and structure the CPTO's day for maximum impact.

### Step 0: Load Context

Read these files:
- `.claude/product-context/team-info.md` — Who to check in with
- `.claude/product-context/strategic-goals.md` — What matters strategically
- `.claude/product-context/current-roadmap.md` — What's in flight
- `.agents/skills/cpto-briefing/SKILL.md` — Severity thresholds

### Step 1: Gather Signals

**If running standalone (no prior briefing context):**
Do lightweight pulls — just the critical signals:
1. Query Jira for blocked items across all projects:
   - `project in (LINK, DATA) AND status = "Blocked" AND sprint in openSprints()`
2. Query Jira for high-priority items:
   - `project in (LINK, DATA) AND priority in (High, Highest) AND status != Done AND sprint in openSprints()`
3. Check Asana bug tracker (project 1200112298205290) for critical bugs

**If running as part of /morning-briefing:**
Use the team-health, product-pulse, and strategic-check outputs already generated in this conversation. Do NOT re-query the same data. Synthesize what's already been surfaced.

### Step 2: Prioritize Actions

Apply this priority framework:

| Priority | Category | Criteria |
|----------|----------|----------|
| **P0** | Unblock Others | Someone is waiting on you. A team is blocked by a decision only you can make. |
| **P1** | Strategic Risk | A strategic priority is off track. A key initiative needs course correction. |
| **P2** | Product Signal | A metric is trending wrong. A feature launch needs attention. |
| **P3** | Proactive | Build relationships, set direction, prepare for upcoming decisions. |

### Step 3: Produce the Day Plan

```markdown
## My Day — {date}

### 30-Second Read
- **Overall health:** {one sentence}
- **Biggest risk:** {one sentence}
- **#1 action today:** {one sentence}
- **Good news:** {one sentence}

---

### Top 3 Actions Today

1. **[P{N}] {Action}**
   - Why: {context}
   - Who: {person to talk to}
   - When: {timing recommendation — morning/afternoon/async}

2. **[P{N}] {Action}**
   - Why: {context}
   - Who: {person}
   - When: {timing}

3. **[P{N}] {Action}**
   - Why: {context}
   - Who: {person}
   - When: {timing}

---

### Unblock Queue
People or teams waiting on you:

| Who | What They Need | Impact of Delay | Suggested Response |
|-----|---------------|-----------------|-------------------|

---

### Recommended Check-ins

| Person | Role | Topic | Format | Priority |
|--------|------|-------|--------|----------|
| {name} | {role} | {what to discuss} | Slack/Call/In-person | {P0-P3} |

---

### Meeting Prep
If you have meetings today, here's context:

| Meeting | Key Context | Your Goal | Watch For |
|---------|------------|-----------|-----------|

> Note: Calendar integration is not available. Review your calendar manually and match meetings to the context above.

---

### Watch List
Things that aren't urgent today but you should track this week:

| Signal | Why It Matters | Check Again |
|--------|---------------|-------------|

---

### Data Gaps
Information you should try to get today:

| Gap | Why You Need It | Who Has It |
|-----|----------------|-----------|
```

### Step 4: Close with One Line

End with a single bold sentence: **"First thing: {the one thing to do before anything else today}."**
