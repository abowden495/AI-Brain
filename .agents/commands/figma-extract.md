---
description: Extract design tokens and styles from Figma
allowed-tools: figma:*
argument-hint: "[Figma URL] [format: css|json|tailwind]"
---

# Figma Design Token Extractor

Extract design tokens (colors, typography, spacing) from a Figma file.

## Your Task

Based on the input: "$ARGUMENTS"

### 1. Parse Input

Extract from arguments:
- **File key or URL**: Required
- **Output format**: css (default), json, tailwind, scss

### 2. Get File Styles

Retrieve all styles from the file:
- Color styles (fills, strokes)
- Text styles (typography)
- Effect styles (shadows, blurs)

### 3. Get Variables (if available)

Check for Figma variables:
- Color variables
- Number variables (spacing, sizing)
- String variables

### 4. Extract and Format

#### CSS Variables (default)
```css
:root {
  /* Colors */
  --color-primary: #0066FF;
  --color-secondary: #6B7280;

  /* Typography */
  --font-family-body: 'Inter', sans-serif;
  --font-size-sm: 14px;
  --font-size-md: 16px;
  --font-size-lg: 18px;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-normal: 1.5;

  /* Spacing */
  --spacing-xs: 4px;
  --spacing-sm: 8px;
  --spacing-md: 16px;
  --spacing-lg: 24px;

  /* Effects */
  --shadow-sm: 0 1px 2px rgba(0,0,0,0.1);
  --shadow-md: 0 4px 6px rgba(0,0,0,0.1);
}
```

#### JSON Tokens
```json
{
  "color": {
    "primary": { "value": "#0066FF", "type": "color" },
    "secondary": { "value": "#6B7280", "type": "color" }
  },
  "fontSize": {
    "sm": { "value": "14px", "type": "dimension" },
    "md": { "value": "16px", "type": "dimension" }
  },
  "spacing": {
    "xs": { "value": "4px", "type": "dimension" },
    "sm": { "value": "8px", "type": "dimension" }
  }
}
```

#### Tailwind Config
```javascript
module.exports = {
  theme: {
    colors: {
      primary: '#0066FF',
      secondary: '#6B7280',
    },
    fontSize: {
      sm: '14px',
      md: '16px',
      lg: '18px',
    },
    spacing: {
      xs: '4px',
      sm: '8px',
      md: '16px',
      lg: '24px',
    },
    boxShadow: {
      sm: '0 1px 2px rgba(0,0,0,0.1)',
      md: '0 4px 6px rgba(0,0,0,0.1)',
    },
  },
}
```

### 5. Naming Conventions

Convert Figma style names to tokens:
- `Primary/Blue` → `--color-primary-blue`
- `Heading/Large` → `--font-size-heading-large`
- Remove special characters
- Use kebab-case

## Output

Present extracted tokens in requested format with:
- Clear categories (colors, typography, spacing, effects)
- Original Figma style names as comments
- Count of tokens extracted

## Notes

- If no URL provided, ask for one
- Default to CSS variables format
- Group related tokens together
- Include original Figma names for reference
