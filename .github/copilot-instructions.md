# HAP Intrinsic Layout Project - CSS Standards

## CRITICAL: Read these rules FIRST before generating any code

### CSS Colors (MANDATORY)
- ALWAYS use hsl() format: `hsl(210, 50%, 50%)`
- NEVER use hex (#3498db) or rgb()
- NEVER use named colors (blue, red, etc.)
- Define colors as CSS custom properties in :root
- Example: `:root { --primary-color: hsl(210, 76%, 54%); }`

### Layout Philosophy (from Stations 1-5)
- **Primary**: CSS Grid for two-dimensional layouts
- **Secondary**: Flexbox for one-dimensional layouts
- **Intrinsic sizing**: Use `minmax()`, `auto-fit`, `auto-fill`
- **Container queries**: Prefer `@container` over `@media` for components
- **Fluid spacing**: Use `clamp()` with computed slopes (base + vw), NEVER arbitrary percentages

### Spacing Standards (Station 3)
- Use CSS custom properties for spacing: `--space-xs` through `--space-xl`
- ALWAYS use `clamp()` for fluid spacing with computed slope formula
- NEVER use fixed pixels: NO `padding: 24px`
- Example: `padding: clamp(1rem, 0.5rem + 1vw, 1.5rem)`

### Grid Patterns (Station 4)
- Use magic pattern: `repeat(auto-fit, minmax(16rem, 1fr))`
- NEVER use fixed column counts: NO `repeat(3, 1fr)`
- Use `fr` units, not percentages
- Example: `grid-template-columns: repeat(auto-fit, minmax(var(--grid-item-min), 1fr))`

### Container Queries (Station 5)
- Components use `@container`, NOT `@media`
- Set `container-type: inline-size` on parent
- Use container units (`cqi`, `cqmin`) for component-relative spacing
- Example: `padding: clamp(1rem, 0.5rem + 2cqi, 3rem)`

### Terminology (IMPORTANT)
- Say "CSS custom property" NEVER "CSS variable"
- Say "intrinsic layout" NEVER "responsive layout"
- Say "container query" NOT "element query"

### HTML Standards
- Use semantic HTML5 elements (<header>, <nav>, <main>, <footer>)
- Avoid unnecessary wrapper divs
- Maximum 3 levels of nesting for layout containers
- All images need alt, width, height attributes

### Accessibility (WCAG 2.2 Level AA REQUIRED)
- All interactive elements keyboard accessible
- Proper heading hierarchy (no skipping levels: h1 → h2 → h3)
- Color contrast: 4.5:1 for normal text, 3:1 for large text
- ARIA labels on navigation landmarks

## What to AVOID (Old CSS patterns)
- ❌ Fixed pixel widths: NO `width: 300px`
- ❌ Fixed pixel spacing: NO `padding: 24px`
- ❌ Hex colors: NO `#3498db`
- ❌ rgb/rgba: NO `rgb(52, 152, 219)`
- ❌ Named colors: NO `background: blue`
- ❌ float or clearfix patterns
- ❌ Viewport media queries in components: NO `@media (min-width: 768px)` for cards/widgets
- ❌ Fixed Grid columns: NO `repeat(3, 1fr)`
- ❌ Excessive nesting: NO 4+ wrapper divs

## Modern CSS Examples (USE THESE)

### Color System
```css
:root {
  --primary-color: hsl(210, 76%, 54%);
  --text-color: hsl(0, 0%, 20%);
  --bg-color: hsl(0, 0%, 98%);
}

.button {
  background: var(--primary-color);
  color: var(--text-color);
}
```

### Intrinsic Grid Pattern
```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr));
  gap: clamp(1rem, 0.5rem + 1.25vw, 2.5rem);
}
```

### Container Query Pattern
```css
.card-container {
  container-type: inline-size;
}

.card {
  padding: clamp(1rem, 0.5rem + 2cqi, 3rem);
}

@container (min-width: 400px) {
  .card {
    flex-direction: row;
  }
}