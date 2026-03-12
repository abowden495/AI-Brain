---
description: Build and run BigQuery SQL queries from natural language
argument-hint: <describe what data you want to query>
allowed-tools: bigquery:*
---

# BigQuery Query Builder

Convert natural language requests into BigQuery SQL queries and execute them.

## Your Task

The user wants to query BigQuery. Help them by:

1. **Understand the request**: Parse what data they're looking for
2. **Identify the table**: If not specified, use `list_tables` to find likely candidates
3. **Check the schema**: Use `describe_table` to understand available columns and partitioning
4. **Estimate cost**: Use `dry_run` to validate the query and show bytes to be processed
5. **Build and execute**: Run the query with `query` and explain what was returned

## Query Building Guidelines

- Always show the SQL you're about to run before executing
- Use `dry_run` first for queries on large tables to estimate cost
- Select only needed columns instead of `SELECT *`
- Apply LIMIT when exploring (default to 100)
- Filter on partition columns when available (crucial for cost)
- Use parameterized queries for user-provided values

## Cost Awareness

- Always note the bytes processed and estimated cost
- Warn if query will scan large amounts of data
- Suggest adding partition filters if missing
- Point out if cache was used (free!)

## Examples

User: "Show me the 10 most recent orders"
→ SQL: `SELECT * FROM \`project.dataset.orders\` ORDER BY created_at DESC LIMIT 10`

User: "Count users by country"
→ SQL: `SELECT country, COUNT(*) as user_count FROM \`project.dataset.users\` GROUP BY country ORDER BY user_count DESC`

User: "Find all orders over $100 from January 2024"
→ SQL with partition filter:
```sql
SELECT * FROM `project.dataset.orders`
WHERE amount > 100
  AND DATE(order_date) BETWEEN '2024-01-01' AND '2024-01-31'
LIMIT 100
```

## User Request

$ARGUMENTS
