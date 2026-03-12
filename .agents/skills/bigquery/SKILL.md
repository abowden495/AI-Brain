---
name: bigquery
description: Provides BigQuery database expertise for exploring schemas, writing SQL queries, and analyzing data. Use this skill when the user asks about BigQuery queries, needs to explore datasets, wants to understand table schemas, or needs help writing analytical SQL.
---

# BigQuery Database Assistant

This skill leverages the BigQuery MCP server to provide intelligent database operations.

## Available MCP Tools

The following tool is available via the BigQuery MCP server (`@ergut/mcp-bigquery-server`):

| Tool | Purpose |
|------|---------|
| `query` | Run a read-only BigQuery SQL query |

**Parameters:**
- `sql` (required) - The SQL query to execute
- `maximumBytesBilled` (optional) - Max bytes billed, defaults to 1GB

**Safety:** Blocks INSERT, UPDATE, DELETE, CREATE, DROP, ALTER, MERGE, TRUNCATE, and other write operations.

## Workflow: Exploring a BigQuery Project

When a user wants to explore BigQuery data, use SQL queries:

1. **List datasets**:
   ```sql
   SELECT schema_name FROM INFORMATION_SCHEMA.SCHEMATA
   ```

2. **List tables** in a dataset:
   ```sql
   SELECT table_name, table_type FROM `project.dataset.INFORMATION_SCHEMA.TABLES`
   ```

3. **Get table schema**:
   ```sql
   SELECT column_name, data_type, is_nullable
   FROM `project.dataset.INFORMATION_SCHEMA.COLUMNS`
   WHERE table_name = 'your_table'
   ```

4. **Sample data**:
   ```sql
   SELECT * FROM `project.dataset.table` LIMIT 10
   ```

## SQL Syntax Reference

### Basic Queries
```sql
-- Select with filter
SELECT * FROM `project.dataset.table`
WHERE status = 'active'
LIMIT 100;

-- Aggregate with grouping
SELECT category, COUNT(*) as count
FROM `project.dataset.table`
GROUP BY category
ORDER BY count DESC;

-- Date filtering (common for partitioned tables)
SELECT *
FROM `project.dataset.table`
WHERE DATE(created_at) >= '2024-01-01';
```

### Parameterized Queries
Use named parameters to avoid SQL injection:
```sql
SELECT * FROM `project.dataset.users`
WHERE email = @email
```
Pass params: `{"email": "user@example.com"}`

### Working with Partitioned Tables
```sql
-- Always filter on partition column for cost efficiency
SELECT *
FROM `project.dataset.events`
WHERE _PARTITIONDATE >= '2024-01-01'
  AND _PARTITIONDATE < '2024-02-01';
```

### Common Functions
```sql
-- Date functions
DATE(timestamp_column)
DATE_TRUNC(date_column, MONTH)
DATE_DIFF(date1, date2, DAY)
FORMAT_DATE('%Y-%m', date_column)

-- String functions
LOWER(string_column)
REGEXP_CONTAINS(string_column, r'pattern')
SPLIT(string_column, ',')

-- Aggregations
COUNT(DISTINCT column)
SUM(IF(condition, value, 0))
ARRAY_AGG(column ORDER BY sort_col)

-- Window functions
ROW_NUMBER() OVER (PARTITION BY group_col ORDER BY sort_col)
SUM(value) OVER (ORDER BY date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW)
```

### JOINs
```sql
SELECT a.*, b.field
FROM `project.dataset.table_a` a
LEFT JOIN `project.dataset.table_b` b
  ON a.id = b.foreign_id;
```

### CTEs (Common Table Expressions)
```sql
WITH filtered_data AS (
  SELECT *
  FROM `project.dataset.table`
  WHERE status = 'active'
),
aggregated AS (
  SELECT category, COUNT(*) as count
  FROM filtered_data
  GROUP BY category
)
SELECT * FROM aggregated
ORDER BY count DESC;
```

## Cost Optimization Tips

1. **Always use dry_run first** - Check bytes processed before running large queries
2. **Filter on partition columns** - Reduces data scanned significantly
3. **Select only needed columns** - Avoid SELECT * for wide tables
4. **Use LIMIT during exploration** - Prevent accidental full table scans
5. **Check cache hits** - Repeated queries may use cached results (free)

## Common Patterns

### Top N Analysis
```sql
SELECT category, SUM(amount) as total
FROM `project.dataset.orders`
GROUP BY category
ORDER BY total DESC
LIMIT 10;
```

### Time Series Aggregation
```sql
SELECT
  DATE_TRUNC(created_at, MONTH) as month,
  COUNT(*) as count
FROM `project.dataset.events`
WHERE created_at >= '2024-01-01'
GROUP BY month
ORDER BY month;
```

### Deduplication
```sql
SELECT * EXCEPT(row_num)
FROM (
  SELECT *,
    ROW_NUMBER() OVER (PARTITION BY id ORDER BY updated_at DESC) as row_num
  FROM `project.dataset.table`
)
WHERE row_num = 1;
```

## Limitations

- Read-only: No INSERT, UPDATE, DELETE, or DDL operations
- Max 1000 rows per query result
- 30 second query timeout
- Blocked operations: CREATE, DROP, ALTER, TRUNCATE, MERGE
