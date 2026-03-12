---
description: Show MongoDB tools and query syntax reference
---

# MongoDB Quick Reference

## Available Commands

| Command | Description |
|---------|-------------|
| `/mongo-explore` | Interactively explore databases, collections, and schemas |
| `/mongo-query <request>` | Build and run queries from natural language |
| `/mongo-aggregate <request>` | Build aggregation pipelines for complex analysis |
| `/mongo-help` | Show this reference |

## Available MCP Tools

### Discovery
- `list-databases` - List all databases
- `list-collections` - List collections in a database
- `collection-schema` - Infer document schema
- `collection-indexes` - Show collection indexes

### Querying
- `find` - Query documents
- `aggregate` - Run aggregation pipelines
- `explain` - Analyze query performance
- `export` - Export results as EJSON

### Stats
- `db-stats` - Database statistics
- `collection-storage-size` - Collection size info

## Quick Query Examples

```json
// Find by field
{"status": "active"}

// Comparison
{"age": {"$gt": 21}}

// Multiple conditions
{"$and": [{"status": "active"}, {"age": {"$gte": 18}}]}

// Pattern matching
{"email": {"$regex": "@gmail.com$"}}

// Array contains
{"tags": "featured"}
```

## Quick Aggregation Examples

```json
// Count by group
[{"$group": {"_id": "$category", "count": {"$sum": 1}}}]

// Top 10 by score
[{"$sort": {"score": -1}}, {"$limit": 10}]

// Filter then group
[{"$match": {"status": "completed"}}, {"$group": {"_id": "$userId", "total": {"$sum": "$amount"}}}]
```

## Tips

1. Use `/mongo-explore` first to understand your data
2. Use projections to limit returned fields
3. Always use `limit` when exploring
4. Check indexes before complex queries
