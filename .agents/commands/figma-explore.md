---
description: Explore Figma files, pages, and frames
allowed-tools: figma:*
argument-hint: "[Figma URL or file key]"
---

# Figma Design Explorer

Explore a Figma design file to understand its structure, pages, frames, and components.

## Your Task

Based on the input: "$ARGUMENTS"

### 1. Parse the Figma Reference

If a URL is provided, extract:
- **File key**: The ID after `/design/` or `/file/`
- **Node ID**: From `?node-id=X-Y` parameter (if present)

URL patterns:
- `https://www.figma.com/design/{file_key}/...`
- `https://www.figma.com/file/{file_key}/...`

### 2. Get File Overview

Retrieve the file and display:
- File name and last modified date
- List of pages
- Key frames on each page
- Component count

### 3. If Node ID Provided

Drill into the specific node:
- Show node type (frame, component, etc.)
- List children and their types
- Show layout properties
- List applied styles

### 4. Identify Design System Elements

Look for:
- Published components
- Published styles (colors, text, effects)
- Component variants
- Auto-layout patterns

## Output Format

```markdown
## File: [File Name]
Last modified: [date]

### Pages
1. **Page Name** - X frames
   - Frame A (node-id: 1-234)
   - Frame B (node-id: 1-235)

### Components (X total)
- ComponentName (node-id: 1-100)
- AnotherComponent (node-id: 1-101)

### Styles
- Colors: X defined
- Text styles: X defined
- Effects: X defined
```

## Notes

- If no URL/key provided, ask the user for a Figma file URL
- Use node IDs to reference specific elements
- Highlight design system patterns found
