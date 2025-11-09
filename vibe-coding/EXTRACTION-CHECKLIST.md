# Design Extraction Checklist

Use this checklist when analyzing websites to ensure you capture everything needed for perfect replication.

## 🎨 Color System

### Primary Colors
- [ ] Primary color(s) with hex codes
- [ ] Secondary color(s) with hex codes
- [ ] Accent color(s) with hex codes
- [ ] Neutral scale (blacks, grays, whites)

### Semantic Colors
- [ ] Success color
- [ ] Warning color
- [ ] Error color
- [ ] Info color

### Usage Patterns
- [ ] Background colors (and when each is used)
- [ ] Text colors (hierarchy: primary, secondary, tertiary)
- [ ] Button colors (all variants)
- [ ] Border/divider colors
- [ ] Overlay colors (with opacity values)

### Special Effects
- [ ] Gradients (direction, stops, colors)
- [ ] Color opacity/alpha values
- [ ] Hover state color changes

## 📝 Typography

### Font Families
- [ ] Primary font name and fallback stack
- [ ] Secondary font (if any)
- [ ] Monospace font (if used for code/technical)
- [ ] Font weights available

### Type Scale
- [ ] H1: size, weight, line-height, letter-spacing
- [ ] H2: size, weight, line-height, letter-spacing
- [ ] H3: size, weight, line-height, letter-spacing
- [ ] H4-H6 (if used)
- [ ] Body: size, weight, line-height
- [ ] Small/Caption: size, weight, line-height
- [ ] Button text: size, weight

### Hierarchy & Patterns
- [ ] How headlines create hierarchy
- [ ] Responsive scaling (desktop vs mobile)
- [ ] Special text treatments (all caps, underlines, etc.)
- [ ] Link styling (color, underline, hover effect)

## 📏 Spacing & Layout

### Spacing System
- [ ] Base spacing unit (4px, 8px, etc.)
- [ ] Full spacing scale
- [ ] Section padding (vertical and horizontal)
- [ ] Component internal spacing
- [ ] Grid gutters

### Layout Structure
- [ ] Container max-width
- [ ] Grid system (12-col, custom, etc.)
- [ ] Breakpoints (mobile, tablet, desktop)
- [ ] Section layouts (full-width, contained, etc.)
- [ ] Common spacing patterns

### Responsive Behavior
- [ ] Mobile layout adaptations
- [ ] Tablet layout adaptations
- [ ] How spacing scales across breakpoints

## 🧩 Components

### Buttons
- [ ] Primary button: colors, padding, radius, font
- [ ] Secondary button: style differences
- [ ] Ghost/text button (if present)
- [ ] Button states: default, hover, active, disabled, focus
- [ ] Button shadows
- [ ] Transition timings

### Cards
- [ ] Card background color
- [ ] Border style and color
- [ ] Border radius
- [ ] Internal padding
- [ ] Shadow
- [ ] Hover effects

### Forms
**Inputs**
- [ ] Input background
- [ ] Border style and color
- [ ] Border radius
- [ ] Padding
- [ ] Font size
- [ ] Focus state (border, shadow, outline)
- [ ] Error state
- [ ] Disabled state

**Labels**
- [ ] Position (above, inline, floating)
- [ ] Font size and weight
- [ ] Color
- [ ] Spacing from input

**Validation**
- [ ] Error message styling
- [ ] Success state styling
- [ ] Inline validation patterns

### Navigation
- [ ] Nav type (horizontal, sidebar, overlay)
- [ ] Nav background and border
- [ ] Link styling (default and active)
- [ ] Spacing between links
- [ ] Hover effects
- [ ] Mobile navigation (hamburger, drawer, etc.)

### Other Components
- [ ] Badge/tag styling
- [ ] Tooltip design
- [ ] Modal/dialog styling
- [ ] Dropdown menus
- [ ] Tables (if present)
- [ ] Lists
- [ ] Dividers/separators

## ✨ Visual Effects

### Shadows
- [ ] Subtle shadow (for slight elevation)
- [ ] Medium shadow (cards)
- [ ] Large shadow (modals, dropdowns)
- [ ] Button shadows
- [ ] Glow effects

### Borders
- [ ] Standard border width
- [ ] Border colors
- [ ] Border radius scale (small, medium, large, full)
- [ ] Divider styles

### Gradients
- [ ] All gradients used (copy exact values)
- [ ] Gradient directions
- [ ] Where each gradient is applied

### Special Effects
- [ ] Backdrop blur (glassmorphism)
- [ ] Background patterns
- [ ] Texture overlays
- [ ] Blend modes
- [ ] Filters

## 🎬 Animations & Interactions

### Transitions
- [ ] Default transition timing
- [ ] Default easing function
- [ ] Fast transition (for small elements)
- [ ] Slow transition (for major changes)

### Hover Effects
- [ ] Button hover (color, transform, shadow)
- [ ] Card hover
- [ ] Link hover
- [ ] Image hover
- [ ] Icon hover

### Scroll Animations
- [ ] Fade in patterns
- [ ] Slide in directions
- [ ] Parallax effects
- [ ] Scroll-triggered animations

### Micro-interactions
- [ ] Loading states
- [ ] Success/error feedback
- [ ] Toggle switches
- [ ] Checkbox/radio animations
- [ ] Menu open/close

### Keyframe Animations
- [ ] Specific named animations
- [ ] Animation durations
- [ ] Loop behavior
- [ ] Delay patterns

## 🎯 Design Patterns

### Overall Vibe
- [ ] Design style (minimal, brutalist, glassmorphic, etc.)
- [ ] Aesthetic keywords (modern, playful, corporate, etc.)
- [ ] Primary mood/feeling

### Key Characteristics
- [ ] Signature design elements
- [ ] Unique visual treatments
- [ ] Common patterns (rounded corners, flat design, etc.)
- [ ] Whitespace usage (generous, tight, balanced)

### Special Elements
- [ ] Custom cursors
- [ ] Animated backgrounds
- [ ] 3D elements
- [ ] Illustrations
- [ ] Icons style
- [ ] Image treatments (filters, overlays)

## 🔧 Technical Details

### Assets
- [ ] Icon library used (or custom)
- [ ] Illustration style
- [ ] Image aspect ratios
- [ ] SVG usage patterns

### Responsive Images
- [ ] Image sizing strategy
- [ ] Lazy loading patterns
- [ ] Placeholder styles

### Performance
- [ ] Font loading strategy
- [ ] Critical CSS patterns
- [ ] Animation performance considerations

## ♿ Accessibility

### Contrast
- [ ] Text contrast ratios (WCAG compliance)
- [ ] Interactive element contrast
- [ ] Focus indicators visibility

### Focus States
- [ ] Focus ring style
- [ ] Focus ring color
- [ ] Focus ring width
- [ ] Keyboard navigation support

### Motion
- [ ] Reduced motion considerations
- [ ] Animation alternatives

## 📱 Responsive Patterns

### Mobile (< 640px)
- [ ] Layout changes
- [ ] Typography scaling
- [ ] Spacing reduction
- [ ] Navigation adaptation
- [ ] Hidden/shown elements

### Tablet (640px - 1024px)
- [ ] Grid changes (columns)
- [ ] Component sizing
- [ ] Spacing adjustments

### Desktop (> 1024px)
- [ ] Maximum widths
- [ ] Multi-column layouts
- [ ] Hover states (desktop only)

## 🎁 Bonus Extraction

### Brand Elements
- [ ] Logo treatment
- [ ] Brand patterns
- [ ] Signature visual elements

### Content Patterns
- [ ] Image-to-text ratios
- [ ] Content hierarchy
- [ ] Call-to-action placement

### User Experience
- [ ] Information architecture
- [ ] User flow patterns
- [ ] Interaction patterns

---

## Usage

1. **Print or Copy this checklist** before analyzing a design
2. **Go through each section** systematically
3. **Document everything** you find
4. **Cross-reference** with browser devtools for exact values
5. **Take screenshots** of states that are hard to capture (hover, focus, etc.)
6. **Test responsive** behavior at different breakpoints
7. **Compile into JSON** design profile when complete

## Pro Tips

✅ Use browser DevTools to inspect actual CSS values
✅ Take screenshots of different states (hover, active, focus)
✅ Test at multiple screen sizes
✅ Note what's NOT there (sometimes absence is intentional)
✅ Document edge cases (very long text, empty states, errors)
✅ Check both light and dark themes if applicable
✅ Review on different devices/browsers for consistency

## Quick Extraction Commands

```
"Extract all button variants from this page"
"What's the complete color system?"
"Document the typography scale"
"List all spacing values used"
"Capture all animation timings"
"Get the complete component library"
```

---

**Happy extracting!** Use this checklist to ensure you capture every design detail for pixel-perfect replication.
