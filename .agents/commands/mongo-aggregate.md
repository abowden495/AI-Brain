---
description: Build MongoDB aggregation pipelines for complex data analysis
argument-hint: <describe the analysis you need>
allowed-tools: mongodb:*
---

# MongoDB Aggregation Builder

Help build and execute MongoDB aggregation pipelines for complex data analysis.

## Your Task

The user needs to perform complex data analysis. Help them by:

1. **Understand the goal**: What insight or transformation do they need?
2. **Check the schema**: Use `collection-schema` to understand the data structure
3. **Design the pipeline**: Build the aggregation pipeline step by step
4. **Explain each stage**: Describe what each stage does
5. **Execute and analyze**: Run the pipeline and interpret results

## Pipeline Stage Reference

| Stage | Purpose |
|-------|---------|
| `$match` | Filter documents (put early for performance) |
| `$group` | Group by field and compute aggregates |
| `$sort` | Order results |
| `$limit` | Limit output count |
| `$project` | Reshape documents, include/exclude fields |
| `$addFields` | Add computed fields |
| `$unwind` | Flatten arrays into separate documents |
| `$lookup` | Join with another collection |
| `$facet` | Run multiple pipelines in parallel |

## Common Aggregations

**Count by category:**
```json
[{"$group": {"_id": "$category", "count": {"$sum": 1}}}]
```

**Sum and average:**
```json
[{"$group": {"_id": "$type", "total": {"$sum": "$amount"}, "avg": {"$avg": "$amount"}}}]
```

**Top N by value:**
```json
[{"$sort": {"score": -1}}, {"$limit": 10}]
```

**Date grouping:**
```json
[{"$group": {"_id": {"$dateToString": {"format": "%Y-%m", "date": "$createdAt"}}, "count": {"$sum": 1}}}]
```

## Instructions

- Show the pipeline before executing so the user can review
- Explain each stage in plain language
- Start simple and add complexity only as needed
- Always include `$limit` to avoid returning too much data

## User Request

$ARGUMENTS
