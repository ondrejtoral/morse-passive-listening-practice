# OK1TRL Design System
## Retro Terminal/BBS Aesthetic Guidelines

This document defines the design language for OK1TRL online tools, inspired by packet radio and BBS-era terminal interfaces.

---

## Design Philosophy

**Terminal-first aesthetic** - All interfaces should evoke the feel of vintage computer terminals, packet radio TNC interfaces, and dial-up BBS systems from the 1980s-90s amateur radio era.

**Core principles:**
- Monospace typography exclusively
- High contrast (black backgrounds, amber/white text)
- CRT-inspired visual effects (scanlines, phosphor glow)
- Minimalist, functional design
- Terminal-style formatting and prefixes
- No gradients, shadows (except glow effects), or modern UI patterns

---

## Color Palette

### Primary Colors
```
--terminal-bg:              #000000   (Pure black background)
--terminal-bg-alt:          #0a0a0a   (Slightly lighter for alternating sections)
--terminal-text:            #e0e0e0   (Primary text - light gray)
--terminal-text-bright:     #ffffff   (Emphasized text - pure white)
```

### Accent Colors
```
--terminal-amber:           #FFBF00   (Primary accent - amber/gold)
--terminal-amber-bright:    #FF9500   (Brighter amber for highlights)
--terminal-green:           #00ff00   (Classic terminal green - optional use)
```

### UI Elements
```
--terminal-border:          #333333   (Borders, dividers, lines)
```

### Usage Guidelines
- **Black (`#000000`)**: All backgrounds
- **Light gray (`#e0e0e0`)**: Body text, standard content
- **White (`#ffffff`)**: Headings, emphasized text, strong elements
- **Amber (`#FFBF00`)**: Links, headings, dates, accents, navigation highlights
- **Bright amber (`#FF9500`)**: Hover states, active elements
- **Green (`#00ff00`)**: Optional for status indicators or special highlights

---

## Typography

### Font Stack
```css
font-family: 'Consolas', 'Courier New', 'Monaco', 'Lucida Console', monospace;
```

**Always use monospace fonts.** This is non-negotiable for the terminal aesthetic.

### Type Scale

| Element | Size | Weight | Color | Letter Spacing |
|---------|------|--------|-------|----------------|
| **Hero/Callsign** | 3rem (48px) | 700 | White | 0.2em |
| **Section Headings (h2)** | 2rem (32px) | 700 | Amber | 0.1em |
| **Subsection Headings (h3)** | 1.3rem (~21px) | 700 | White | normal |
| **Body Text** | 1rem (16px) | 400 | Light gray | normal |
| **Small Text** | 0.85-0.9rem | 400 | Light gray | normal |

### Text Formatting

**Heading Prefixes** (Terminal-style prompt characters):
```css
h2::before { content: '> '; }      /* Level 1 headings */
h3::before { content: '>> '; }     /* Level 2 headings */
```

**Date/Timestamp Format**:
```css
.date::before { content: '['; }
.date::after { content: ']'; }
```
Example: `[2026-01]` or `[3D DESIGN]`

**Navigation Items**:
Wrap in brackets: `[ABOUT]`, `[PROJECTS]`, `[CONTACT]`

**List Items** (when using custom lists):
```css
li::before { content: '* '; color: var(--terminal-amber); }
```

---

## Visual Effects

### CRT Scanline Effect
```css
body::before {
    content: '';
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    pointer-events: none;
    background: repeating-linear-gradient(
        0deg,
        rgba(0, 0, 0, 0.15),
        rgba(0, 0, 0, 0.15) 1px,
        transparent 1px,
        transparent 2px
    );
    z-index: 9999;
}
```
Apply this as a fixed overlay on the entire page for the CRT effect.

### Phosphor Glow
```css
body {
    text-shadow: 0 0 1px rgba(224, 224, 224, 0.3);
}

/* For emphasized elements (like hero text): */
.callsign {
    text-shadow: 0 0 10px rgba(255, 191, 0, 0.5);
}
```

---

## Component Patterns

### Content Boxes (Terminal Windows)
```css
.content-box {
    background-color: #000000;
    padding: 25px;
    border: 1px solid #333333;
    max-width: 900px;
    margin: 0 auto;
}
```

Use for any container holding text content, forms, or grouped information.

### Navigation

**Desktop Navigation:**
- Horizontal bar with items separated by 1px borders
- All-caps text in brackets: `[ABOUT]` `[PROJECTS]`
- Hover state: amber background (#FFBF00) with black text
- No transitions (instant state changes for retro feel)

**Mobile Navigation:**
- Collapsible hamburger menu
- Use terminal-style icons: `[═══]` for closed, `[×××]` for open
- Full-width stacked links with bottom borders

### Links

**Standard Links:**
```css
a {
    color: #FFBF00;
    text-decoration: underline;
}

a:hover, a:focus {
    background-color: #FFBF00;
    color: #000000;
    text-decoration: none;
}
```

### Buttons
Style like navigation items:
```css
button {
    font-family: monospace;
    padding: 12px 20px;
    background-color: transparent;
    border: 1px solid #333333;
    color: #e0e0e0;
    cursor: pointer;
}

button:hover, button:focus {
    background-color: #FFBF00;
    color: #000000;
}
```

### Dividers
```css
/* Solid borders for major sections */
border: 1px solid #333333;

/* Dashed for sub-sections */
border-bottom: 1px dashed #333333;

/* Dotted for list items */
border-bottom: 1px dotted #333333;
```

---

## Layout & Spacing

### Container
```css
.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}
```

### Section Padding
- Desktop: `50px 20px`
- Tablet (≤768px): `35px 15px`
- Mobile (≤480px): Adjust to `25px 15px` if needed

### Content Width
- Primary content boxes: `max-width: 900px`
- Center all content boxes within sections

---

## Interactive States

### Hover Effects
**No smooth transitions** - instant state changes for authentic terminal feel.

**Standard Pattern:**
- Default: Amber text on black background
- Hover: Black text on amber background
- Example: Navigation, links, buttons

### Focus States
Same as hover states for keyboard navigation accessibility.

---

## Responsive Design

### Breakpoints
- **Desktop**: Default styles
- **Tablet**: `@media (max-width: 768px)`
- **Mobile**: `@media (max-width: 480px)`

### Mobile Adjustments
- Reduce font sizes (hero: 2rem → 1.6rem)
- Reduce padding (25px → 18px)
- Collapse navigation to hamburger menu
- Stack all horizontal layouts vertically
- Maintain monospace and terminal aesthetic at all sizes

---

## Accessibility

### High Contrast Mode
```css
@media (prefers-contrast: high) {
    :root {
        --terminal-text: #ffffff;
        --terminal-border: #666666;
    }
}
```

### Best Practices
- Ensure all interactive elements have visible focus states
- Use semantic HTML (`<nav>`, `<main>`, `<section>`, `<header>`, `<footer>`)
- Provide `aria-label` attributes for icon-only buttons
- Maintain color contrast ratios (amber on black: 10:1, white on black: 21:1)
- Keep hit targets at least 44×44px on mobile

---

## Implementation Checklist

When creating a new tool with this design system:

- [ ] Set up CSS variables for color palette
- [ ] Apply monospace font stack to all text
- [ ] Add CRT scanline overlay effect
- [ ] Add subtle phosphor glow to text
- [ ] Use black background throughout
- [ ] Style headings with terminal prefixes (`>` and `>>`)
- [ ] Wrap navigation items and dates in brackets
- [ ] Apply amber hover states to all interactive elements
- [ ] Remove all transitions and animations
- [ ] Add 1px borders (#333333) to content boxes
- [ ] Test on mobile and add hamburger menu if needed
- [ ] Verify focus states for keyboard navigation
- [ ] Test with high contrast mode preference

---

## Examples

### Hero Section
```html
<header class="hero">
    <div class="container">
        <div class="callsign">TOOL NAME</div>
        <p class="tagline">Tool Description</p>
        <div class="location">Additional Info</div>
    </div>
</header>
```

### Section with Content Box
```html
<section class="section">
    <div class="container">
        <h2>Section Title</h2>
        <div class="content-box">
            <h3>Subsection</h3>
            <p>Content here...</p>
        </div>
    </div>
</section>
```

### Date/Timestamp
```html
<span class="date">2026-01</span>
<!-- Renders as: [2026-01] -->
```

### Navigation
```html
<nav class="main-nav">
    <div class="container">
        <ul>
            <li><a href="#section1">[SECTION 1]</a></li>
            <li><a href="#section2">[SECTION 2]</a></li>
        </ul>
    </div>
</nav>
```

---

## Reference Files

- Full implementation: `style.css`
- HTML structure: `index.html`
- Content guidelines: `CLAUDE.md`

---

**73 de OK1TRL**
*Last updated: January 2026*
