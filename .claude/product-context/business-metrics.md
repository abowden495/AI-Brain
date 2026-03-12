# Business Metrics

**Last Updated:** 2026-03-12

## Key Metrics & Data Sources

### Engagement Metrics

| Metric | Definition | Data Source | Target | Alert Threshold |
|--------|-----------|-------------|--------|-----------------|
| DAU / WAU / MAU | Unique users active per period | BigQuery (user activity tables) | Growing W/W | WAU drop >15% W/W |
| Multi-team adoption rate | % enterprise accounts with 2+ distinct teams active weekly | BigQuery + MongoDB | Increasing Q/Q | Flat or declining |
| Session depth | Avg pages/actions per session | BigQuery / Mixpanel | TBD | TBD |
| Feature activation rate | % users who try a feature within 7 days of release | Mixpanel (if available) / BigQuery | >30% | <15% |

### Agentic Capability Metrics

| Metric | Definition | Data Source | Target | Alert Threshold |
|--------|-----------|-------------|--------|-----------------|
| Agentic feature activation | % active accounts using Coach AI, Insights Agent, TALs, or Team Spaces | BigQuery / MongoDB | Majority by EOQ | <25% at mid-Q |
| Scout Agent usage | Queries/enrichments per week | BigQuery (DATA project) | Growing W/W | Flat for 2+ weeks |
| Insights Agent alerts | Insights surfaced per week | BigQuery (DATA project) | Growing | Drop >30% W/W |
| Coach AI sessions | Coaching sessions initiated | BigQuery / MongoDB | Growing | TBD |

### Product Health

| Metric | Definition | Data Source | Target | Alert Threshold |
|--------|-----------|-------------|--------|-----------------|
| Error rate (frontend) | % of sessions with JS errors | Sentry | <2% | >5% |
| Error rate (backend) | 5xx rate per endpoint | Sentry / GCP Monitoring | <0.5% | >2% |
| API latency p95 | 95th percentile response time | GCP Monitoring / BigQuery | <500ms | >1000ms |
| Sentry high-frequency errors | Errors with >1000 occurrences | Sentry | Declining | New high-freq errors |

### Business Metrics

| Metric | Definition | Data Source | Target | Alert Threshold |
|--------|-----------|-------------|--------|-----------------|
| ARR | Annual recurring revenue | Finance / CRM | Growing | N/A |
| NRR | Net revenue retention | Finance / CRM | >120% | <100% |
| Pipeline influenced by product | Deals where product features cited in sales process | CRM / Manual | Growing | N/A |

---

## Data Source Mapping

### Available via MCP

| Source | MCP Tool | What It Provides |
|--------|----------|-----------------|
| BigQuery | `query` (BigQuery MCP) | User analytics, product metrics, data pipeline outputs |
| MongoDB | MongoDB MCP tools | User accounts, feature configs, real-time app state |
| Jira | Jira MCP tools | Sprint health, tickets, velocity, blockers |
| Asana | Asana MCP tools | Product board, bug tracking, cross-functional projects |

### Not Available via MCP (Manual Check Required)

| Source | Access Method | What It Provides |
|--------|--------------|-----------------|
| Mixpanel | Web dashboard / possible BQ export | Event-level product analytics, funnels, retention |
| Sentry | Web dashboard (https://liminal-1m.sentry.io) | Error tracking, crash reports |
| GCP Monitoring | Cloud Console | Infrastructure metrics, latency, uptime |
| Unleash | Web dashboard (https://features.liminal-infra.com) | Feature flag status |
| CRM | Manual | Revenue metrics, pipeline |

---

## BigQuery Tables (Known)

> **GCP Project:** `analyticsdashboard-403720`

| Dataset/Table | Contents | Used By |
|--------------|----------|---------|
| `raw_news` / `tidy_news` | News articles, AI-tagged themes, entities | Market Monitor |
| `raw_market_size` / `tidy_market_size` | Market sizing model data | Advisory / Buyer App |
| INFORMATION_SCHEMA | Schema metadata for exploration | All queries |

> **TODO:** Run `/bq-explore` to discover full dataset/table inventory and map to metrics above.

---

## Mixpanel Status

> **TODO:** Check if Mixpanel data exports to BigQuery (many companies enable this).
> If yes, add BigQuery table references here and `/product-pulse` works immediately.
> If no, Mixpanel metrics will show as "check dashboard manually" in reports.

## MongoDB Collections (Known)

> **TODO:** Run `/mongo-explore` to inventory collections relevant to user activity and feature usage.
