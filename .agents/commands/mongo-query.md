---
description: Build and run MongoDB queries from natural language
argument-hint: <describe what you want to find>
allowed-tools: mongodb:*
---

# MongoDB Query Builder

Convert natural language requests into MongoDB queries and execute them.

## Your Task

The user wants to query MongoDB. Help them by:

1. **Understand the request**: Parse what data they're looking for
2. **Identify the collection**: If not specified, use `list-collections` to find likely candidates
3. **Check the schema**: Use `collection-schema` to understand available fields
4. **Build the query**: Construct the appropriate MongoDB query
5. **Execute and explain**: Run the query with `find` and explain what was returned

## Query Building Guidelines

- Always show the query you're about to run before executing
- Use projections to limit fields when the user only needs specific data
- Apply sensible limits (default to 20) unless the user asks for more
- Use sorting when it makes sense for the data type

## Examples

User: "Find all active users"
→ Query: `{"status": "active"}` on users collection

User: "Show me the 5 most recent orders over $100"
→ Query: `{"total": {"$gt": 100}}` with sort `{"createdAt": -1}` and limit 5

User: "Count how many products are in each category"
→ Aggregation: `[{"$group": {"_id": "$category", "count": {"$sum": 1}}}]`

## User Request

$ARGUMENTS
