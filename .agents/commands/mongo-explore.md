---
description: Explore MongoDB databases, collections, and schemas interactively
allowed-tools: mongodb:*
---

# MongoDB Explorer

Explore the connected MongoDB database to understand its structure.

## Your Task

Guide the user through exploring their MongoDB database:

1. **Start with databases**: Use `list-databases` to show available databases
2. **Show collections**: Once a database is selected, use `list-collections`
3. **Analyze schemas**: For collections of interest, use `collection-schema` to infer the document structure
4. **Check indexes**: Use `collection-indexes` to show optimization options
5. **Sample data**: Use `find` with limit=5 to show example documents

## Instructions

- Be conversational and guide the user through discovery
- Summarize findings in clear, formatted tables when helpful
- Highlight interesting patterns you notice in the data
- Suggest potential queries based on the schema you discover
- If the user provides a specific database or collection name, start there

$ARGUMENTS
