---
description: Show BigQuery tools and SQL syntax reference
---

# BigQuery Quick Reference

## Available Commands

| Command | Description |
|---------|-------------|
| `/bq-explore` | Interactively explore projects, datasets, and table schemas |
| `/bq-query <request>` | Build and run SQL queries from natural language |
| `/bq-help` | Show this reference |

## Available MCP Tools

| Tool | Purpose |
|------|---------|
| `query` | Run a read-only BigQuery SQL query |

**Parameters:** `sql` (required), `maximumBytesBilled` (optional, default 1GB)

### Schema Exploration via SQL

```sql
-- List datasets
SELECT schema_name FROM INFORMATION_SCHEMA.SCHEMATA

-- List tables in a dataset
SELECT table_name, table_type
FROM `project.dataset.INFORMATION_SCHEMA.TABLES`

-- Get table columns
SELECT column_name, data_type, is_nullable
FROM `project.dataset.INFORMATION_SCHEMA.COLUMNS`
WHERE table_name = 'your_table'
```

## Quick SQL Examples

```sql
-- Basic select with filter
SELECT * FROM `project.dataset.table`
WHERE status = 'active'
LIMIT 100;

-- Count by category
SELECT category, COUNT(*) as count
FROM `project.dataset.table`
GROUP BY category
ORDER BY count DESC;

-- Date range filter (important for partitioned tables!)
SELECT * FROM `project.dataset.events`
WHERE DATE(created_at) BETWEEN '2024-01-01' AND '2024-01-31';

-- Parameterized query (use @param_name)
SELECT * FROM `project.dataset.users`
WHERE email = @email
-- Pass params: {"email": "user@example.com"}
```

## Aggregation Examples

```sql
-- Monthly totals
SELECT
  FORMAT_DATE('%Y-%m', date) as month,
  SUM(amount) as total
FROM `project.dataset.orders`
GROUP BY month
ORDER BY month;

-- Top 10 with percentage
SELECT
  category,
  COUNT(*) as count,
  ROUND(100.0 * COUNT(*) / SUM(COUNT(*)) OVER(), 2) as pct
FROM `project.dataset.items`
GROUP BY category
ORDER BY count DESC
LIMIT 10;
```

## Cost-Saving Tips

1. **Use dry_run first** - Always estimate bytes before big queries
2. **Filter on partitions** - Use date filters on partitioned tables
3. **Select specific columns** - Avoid `SELECT *` on wide tables
4. **Use LIMIT** - Especially when exploring data
5. **Check cache** - Query results show if cache was used

## Tips

1. Use `/bq-explore` first to understand your data
2. Always include LIMIT when exploring
3. Use dry_run to estimate costs before running queries
4. Filter on partition columns to reduce bytes scanned
