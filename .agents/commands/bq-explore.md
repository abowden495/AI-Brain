---
description: Explore BigQuery projects, datasets, and table schemas interactively
allowed-tools: bigquery:*
---

# BigQuery Explorer

Explore the connected BigQuery project to understand its structure using SQL queries.

## Your Task

Guide the user through exploring their BigQuery data using the `query` tool:

1. **List datasets**:
   ```sql
   SELECT schema_name FROM INFORMATION_SCHEMA.SCHEMATA
   ```

2. **List tables** in a dataset:
   ```sql
   SELECT table_name, table_type, creation_time, row_count, size_bytes
   FROM `project.dataset.INFORMATION_SCHEMA.TABLE_STORAGE`
   ```

3. **Get table schema**:
   ```sql
   SELECT column_name, data_type, is_nullable, is_partitioning_column
   FROM `project.dataset.INFORMATION_SCHEMA.COLUMNS`
   WHERE table_name = 'table_name'
   ORDER BY ordinal_position
   ```

4. **Sample data**:
   ```sql
   SELECT * FROM `project.dataset.table` LIMIT 10
   ```

## Instructions

- Be conversational and guide the user through discovery
- Summarize findings in clear, formatted tables
- Highlight partitioning columns (important for cost optimization)
- Note table sizes and row counts
- Suggest useful queries based on the schema you discover
- If the user provides a specific dataset or table name, start there

$ARGUMENTS
