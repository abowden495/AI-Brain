---
description: Show Figma tools and workflow reference
---

# Figma Quick Reference

## Available Commands

| Command | Description |
|---------|-------------|
| `/figma-explore` | Explore Figma files, pages, and frames |
| `/figma-extract` | Extract design tokens and styles |
| `/figma-help` | Show this reference |

## Understanding Figma URLs

Figma URLs contain identifiers you'll need:

```
https://www.figma.com/design/ABC123xyz/My-Design?node-id=1-234
                            ^^^^^^^^^                   ^^^^^
                            file_key                    node_id
```

- **File key**: Unique identifier for the file
- **Node ID**: Reference to specific frame/component (format: `X-Y`)

## Common Workflows

### 1. Explore a Design
1. Share Figma URL or file key
2. Get file structure and pages
3. Drill into specific frames

### 2. Extract Design Tokens
1. Get styles from the file
2. Extract colors, typography, spacing
3. Format as CSS/JSON/Tailwind

### 3. Design-to-Code
1. Select frame by URL or node ID
2. Analyze layout and styles
3. Generate component code

## Design Token Types

| Type | What to Extract |
|------|-----------------|
| Colors | Fill styles, stroke colors |
| Typography | Text styles (font, size, weight) |
| Spacing | Auto-layout gaps, padding |
| Effects | Shadows, blurs |
| Sizing | Fixed dimensions, constraints |

## Tips

1. **Copy frame URL** - Right-click frame > Copy link
2. **Use node IDs** - More precise than frame names
3. **Check components** - Indicates design system patterns
4. **Look for styles** - Published styles = design tokens
5. **Dev Mode** - Enable for more accurate specs

## Output Format Options

When extracting tokens:
- **CSS Variables** - For vanilla CSS projects
- **JSON Tokens** - For design token tools
- **Tailwind** - For Tailwind CSS config
- **SCSS** - For Sass projects

## File Structure

Figma files are organized as:
```
File
├── Page 1
│   ├── Frame A
│   │   ├── Component
│   │   └── Text
│   └── Frame B
└── Page 2
    └── Frame C
```
