---
name: mongodb
description: Provides MongoDB database expertise for exploring schemas, writing queries, building aggregation pipelines, and optimizing database operations. Use this skill when the user asks about MongoDB queries, needs to explore a database, wants to understand collection schemas, or needs help with aggregation pipelines.
---

# MongoDB Database Assistant

This skill leverages the MongoDB MCP server to provide intelligent database operations.

## Available MCP Tools

The following tools are available via the MongoDB MCP server:

### Connection & Discovery
| Tool | Purpose |
|------|---------|
| `connect` | Connect to a MongoDB database |
| `list-databases` | List all databases |
| `list-collections` | List collections in a database |

### Schema & Metadata
| Tool | Purpose |
|------|---------|
| `collection-schema` | Infer schema from documents |
| `collection-indexes` | List indexes on a collection |
| `collection-storage-size` | Get collection size stats |
| `db-stats` | Get database statistics |

### Querying Data
| Tool | Purpose |
|------|---------|
| `find` | Query documents with filters, projection, sort, limit |
| `aggregate` | Run aggregation pipelines |
| `explain` | Analyze query execution plans |
| `export` | Export query results in EJSON format |

## Workflow: Exploring a New Database

When a user wants to explore a MongoDB database:

1. **List databases** to see what's available
2. **List collections** in the target database
3. **Get schema** for collections of interest using `collection-schema`
4. **Check indexes** to understand query optimization options
5. **Sample data** using `find` with a small limit

## Query Syntax Reference

### Basic Queries
```json
// Equality
{"status": "active"}

// Comparison operators
{"age": {"$gt": 18}}
{"price": {"$gte": 10, "$lte": 100}}

// Array contains
{"tags": "mongodb"}

// Logical operators
{"$or": [{"status": "active"}, {"featured": true}]}
{"$and": [{"price": {"$gt": 10}}, {"stock": {"$gt": 0}}]}

// Regex matching
{"name": {"$regex": "^John", "$options": "i"}}

// Nested field access
{"address.city": "New York"}

// Existence check
{"email": {"$exists": true}}

// Array operations
{"tags": {"$in": ["mongodb", "database"]}}
{"scores": {"$elemMatch": {"$gt": 80}}}
```

### Projections
```json
// Include specific fields (1 = include)
{"name": 1, "email": 1, "_id": 0}

// Exclude specific fields (0 = exclude)
{"password": 0, "internal": 0}
```

### Sorting
```json
// Ascending (1) and descending (-1)
{"createdAt": -1, "name": 1}
```

## Aggregation Pipeline Patterns

### Group and Count
```json
[
  {"$group": {"_id": "$category", "count": {"$sum": 1}}}
]
```

### Filter, Group, Sort
```json
[
  {"$match": {"status": "completed"}},
  {"$group": {"_id": "$customerId", "total": {"$sum": "$amount"}}},
  {"$sort": {"total": -1}},
  {"$limit": 10}
]
```

### Lookup (Join Collections)
```json
[
  {"$lookup": {
    "from": "orders",
    "localField": "_id",
    "foreignField": "customerId",
    "as": "orders"
  }},
  {"$unwind": "$orders"}
]
```

### Date Aggregations
```json
[
  {"$match": {"createdAt": {"$gte": {"$date": "2024-01-01"}}}},
  {"$group": {
    "_id": {"$dateToString": {"format": "%Y-%m", "date": "$createdAt"}},
    "count": {"$sum": 1}
  }},
  {"$sort": {"_id": 1}}
]
```

### Computed Fields
```json
[
  {"$addFields": {
    "totalPrice": {"$multiply": ["$quantity", "$unitPrice"]},
    "fullName": {"$concat": ["$firstName", " ", "$lastName"]}
  }}
]
```

## Tips for Effective Queries

1. **Always check indexes first** - Use `collection-indexes` before writing complex queries
2. **Use projections** - Only request fields you need to reduce data transfer
3. **Limit results** - Always use `limit` when exploring data
4. **Use explain** - Analyze slow queries with the `explain` tool
5. **Match early** - In aggregation pipelines, put `$match` stages first to reduce documents processed

## Common Patterns

### Pagination
```json
// Page 2 with 20 items per page
{"skip": 20, "limit": 20, "sort": {"_id": 1}}
```

### Text Search (requires text index)
```json
{"$text": {"$search": "coffee shop"}}
```

### Geospatial Query (requires 2dsphere index)
```json
{
  "location": {
    "$near": {
      "$geometry": {"type": "Point", "coordinates": [-73.9667, 40.78]},
      "$maxDistance": 1000
    }
  }
}
```
