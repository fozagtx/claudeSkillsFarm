---
name: vibe-coding
description: Extract and replicate the complete visual aesthetic, design system, and UI vibe from any website or page. Analyzes color palettes, typography, spacing, layout hierarchy, components, animations, and visual patterns to create a comprehensive design profile. Use this skill to clone page aesthetics by pasting a URL or screenshot, then generate the exact prompts and specifications needed to recreate the design in any visual coding tool (v0, Bolt, Lovable, Claude Artifacts, etc.).
---

# Vibe Coding - UI Aesthetic Extraction & Replication

You are a design system extraction specialist that analyzes websites and creates comprehensive design profiles for perfect aesthetic replication.

## How It Works

This skill transforms any website or page into a structured design profile containing every visual element needed to recreate its aesthetic. Users can:

1. **Paste a URL or upload a screenshot**
2. **Get a complete design system analysis**
3. **Receive optimized prompts for vibe coding tools**
4. **Replicate the exact aesthetic in their projects**

## Design Profile Structure

When analyzing a page, extract and document:

```json
{
  "pageInfo": {
    "url": "URL of analyzed page",
    "pageName": "Name/description of page",
    "category": "Landing page/Dashboard/E-commerce/etc",
    "overallVibe": "Minimal/Modern/Brutalist/Playful/Corporate/etc",
    "primaryPurpose": "What the page is designed to achieve"
  },
  "colorSystem": {
    "palette": {
      "primary": ["#HEX1", "#HEX2"],
      "secondary": ["#HEX3", "#HEX4"],
      "accent": ["#HEX5", "#HEX6"],
      "neutrals": ["#HEX7", "#HEX8", "#HEX9"],
      "semantic": {
        "success": "#HEX",
        "warning": "#HEX",
        "error": "#HEX",
        "info": "#HEX"
      }
    },
    "usage": {
      "backgrounds": "Which colors for what type of background",
      "text": "Text color hierarchy and contrast ratios",
      "buttons": "Button color states (default, hover, active)",
      "borders": "Border and divider colors"
    },
    "colorTheory": "Description of color relationships and why they work"
  },
  "typography": {
    "fontFamilies": {
      "primary": {
        "name": "Font name",
        "fallback": "Fallback stack",
        "usage": "Headlines, UI, body",
        "weights": [400, 500, 600, 700]
      },
      "secondary": {
        "name": "Font name",
        "fallback": "Fallback stack",
        "usage": "Specific use cases"
      },
      "mono": {
        "name": "Monospace font if used",
        "usage": "Code, numbers, technical"
      }
    },
    "typeScale": {
      "h1": { "size": "clamp or px", "weight": 700, "lineHeight": 1.2, "letterSpacing": "-0.02em" },
      "h2": { "size": "clamp or px", "weight": 600, "lineHeight": 1.3 },
      "h3": { "size": "clamp or px", "weight": 600, "lineHeight": 1.4 },
      "body": { "size": "clamp or px", "weight": 400, "lineHeight": 1.6 },
      "small": { "size": "clamp or px", "weight": 400, "lineHeight": 1.5 },
      "caption": { "size": "clamp or px", "weight": 400, "lineHeight": 1.4 }
    },
    "hierarchy": "How typography creates visual hierarchy"
  },
  "spacing": {
    "system": "4px/8px base or custom scale",
    "scale": [4, 8, 12, 16, 24, 32, 48, 64, 96, 128],
    "containerMaxWidth": "1280px or custom",
    "sectionPadding": "Vertical spacing between sections",
    "componentSpacing": "Internal component spacing patterns",
    "gutters": "Grid gutter sizes"
  },
  "layout": {
    "grid": {
      "type": "12-column/Custom",
      "maxWidth": "Container width",
      "breakpoints": {
        "mobile": "< 640px",
        "tablet": "640px - 1024px",
        "desktop": "> 1024px"
      }
    },
    "sections": [
      {
        "name": "Hero Section",
        "structure": "Layout description",
        "height": "Viewport height or fixed",
        "alignment": "Center/Left/Right",
        "contentWidth": "Full/Contained"
      }
    ],
    "patterns": "Common layout patterns used (sidebar, cards, split)"
  },
  "components": {
    "buttons": {
      "primary": {
        "background": "Color",
        "text": "Color",
        "border": "Style",
        "borderRadius": "px or rem",
        "padding": "vertical horizontal",
        "fontSize": "Size",
        "fontWeight": "Weight",
        "states": {
          "hover": "Transform/color changes",
          "active": "Press state",
          "disabled": "Disabled appearance"
        },
        "shadow": "Box shadow if any"
      },
      "secondary": { "...": "similar structure" },
      "ghost": { "...": "similar structure" }
    },
    "cards": {
      "style": "Flat/Elevated/Outlined",
      "borderRadius": "Value",
      "padding": "Internal spacing",
      "shadow": "Box shadow",
      "border": "Border style",
      "hoverEffect": "What happens on hover"
    },
    "forms": {
      "inputs": {
        "borderRadius": "Value",
        "border": "Style and color",
        "padding": "Internal spacing",
        "fontSize": "Input text size",
        "focusState": "Border/shadow on focus",
        "errorState": "Error styling"
      },
      "labels": {
        "position": "Above/Inline/Floating",
        "fontSize": "Size",
        "fontWeight": "Weight",
        "spacing": "Distance from input"
      }
    },
    "navigation": {
      "type": "Horizontal/Sidebar/Overlay",
      "style": "Description of nav styling",
      "activeState": "How active links look",
      "spacing": "Link spacing",
      "typography": "Nav link typography"
    }
  },
  "visualEffects": {
    "shadows": {
      "subtle": "box-shadow value",
      "medium": "box-shadow value",
      "large": "box-shadow value"
    },
    "borders": {
      "style": "Solid/Dashed/None",
      "width": "Common widths",
      "radius": {
        "small": "4px",
        "medium": "8px",
        "large": "16px",
        "full": "9999px"
      }
    },
    "gradients": [
      {
        "name": "Primary gradient",
        "value": "linear-gradient(...)",
        "usage": "Where it's used"
      }
    ],
    "blurs": {
      "backdrop": "backdrop-filter value if used",
      "glassmorphism": "Glass effect specs"
    }
  },
  "animations": {
    "transitions": {
      "default": "transition timing",
      "smooth": "slower transition",
      "snappy": "faster transition"
    },
    "keyframes": [
      {
        "name": "Animation name",
        "description": "What it does",
        "duration": "Time",
        "easing": "Ease function"
      }
    ],
    "microInteractions": [
      "Button hover lifts slightly",
      "Icons rotate on hover",
      "Cards scale on hover"
    ]
  },
  "designPatterns": {
    "visualStyle": "Flat/Neumorphic/Glassmorphic/Brutalist/etc",
    "aesthetic": "Minimal/Maximalist/Playful/Corporate/etc",
    "keyCharacteristics": [
      "Bold typography",
      "High contrast",
      "Rounded corners everywhere",
      "Generous whitespace"
    ],
    "uniqueElements": [
      "Custom cursor",
      "Animated backgrounds",
      "3D elements"
    ]
  },
  "ingredients": {
    "essentialElements": [
      "List of components needed to recreate the design",
      "Any special libraries or tools",
      "Icon sets used",
      "Image treatments"
    ],
    "techStack": {
      "detected": "What the page appears to use",
      "recommended": "What you should use to replicate"
    }
  }
}
```

## Usage Instructions

### 1. Analyze a Page

**From URL**:
```
"Analyze the design vibe of [URL] and create a complete design profile"
```

**From Screenshot**:
```
"Extract the design system from this screenshot" [attach image]
```

### 2. Get Vibe Coding Prompt

After analysis:
```
"Create a v0/Bolt/Lovable prompt to replicate this design"
"Generate the exact prompt for recreating the hero section"
```

### 3. Component-Specific Extraction

```
"Extract just the button styling from this page"
"What's the card component design pattern here?"
"Give me the navigation styling specs"
```

## Output Formats

### Complete Design Profile
Full JSON with all design specifications for technical implementation.

### Vibe Coding Prompt
Natural language prompt optimized for AI coding tools:
```
"Create a landing page with these specifications:

**Overall Vibe**: Modern, minimal SaaS with subtle glassmorphism

**Colors**:
- Primary: #6366F1 (Indigo)
- Secondary: #8B5CF6 (Purple)
- Background: #0F172A (Dark blue-gray)
- Accent: #EC4899 (Pink)

**Typography**:
- Font: Inter for everything
- H1: 72px, weight 700, line-height 1.1, tight letter-spacing
- Body: 18px, weight 400, line-height 1.6

**Layout**:
- Full-width hero with centered content
- Max container width: 1280px
- Generous padding: 96px vertical sections

**Key Components**:
- Primary button: Indigo background, white text, 16px rounded corners, subtle shadow, lifts 2px on hover
- Cards: Dark background (#1E293B), 12px border radius, subtle border (#334155), glow effect on hover
- Inputs: Dark with subtle border, purple focus ring

**Visual Effects**:
- Subtle grid pattern in background
- Glassmorphic navigation bar (backdrop blur)
- Gradient overlays on hero
- Smooth transitions (300ms ease)

**Animations**:
- Fade in on scroll for sections
- Hover lift for interactive elements
- Smooth color transitions"
```

### Quick Reference Card
Essential specs for quick implementation:
```
COLORS: Primary #6366F1, Secondary #8B5CF6, BG #0F172A
FONTS: Inter (400, 500, 600, 700)
SPACING: 8px base scale
RADIUS: 12px standard, 16px large
SHADOWS: subtle 0 2px 8px rgba(0,0,0,0.1)
```

## Examples

### Example 1: Modern SaaS Landing Page

**Input**: "Analyze https://linear.app"

**Output**:
```json
{
  "pageInfo": {
    "url": "https://linear.app",
    "pageName": "Linear - Project Management",
    "category": "SaaS Landing Page",
    "overallVibe": "Ultra-minimal, modern, high-contrast with subtle gradients",
    "primaryPurpose": "Convert visitors to sign up for project management tool"
  },
  "colorSystem": {
    "palette": {
      "primary": ["#5E6AD2"],
      "secondary": ["#8B5CF6"],
      "accent": ["#EC4899"],
      "neutrals": ["#000000", "#18181B", "#27272A", "#E4E4E7", "#FFFFFF"],
      "semantic": {
        "success": "#10B981",
        "warning": "#F59E0B",
        "error": "#EF4444"
      }
    },
    "usage": {
      "backgrounds": "Pure black (#000) for hero, dark gray (#18181B) for sections",
      "text": "White for primary (#FFF), gray (#A1A1AA) for secondary",
      "buttons": "Purple gradient primary, white outline secondary",
      "borders": "Subtle gray (#27272A) 1px"
    },
    "colorTheory": "High contrast black/white with vibrant purple accents. Minimal color usage creates focus."
  },
  "typography": {
    "fontFamilies": {
      "primary": {
        "name": "Inter",
        "fallback": "-apple-system, system-ui, sans-serif",
        "usage": "All text",
        "weights": [400, 500, 600]
      }
    },
    "typeScale": {
      "h1": { "size": "clamp(48px, 8vw, 96px)", "weight": 600, "lineHeight": 1, "letterSpacing": "-0.04em" },
      "h2": { "size": "clamp(32px, 5vw, 56px)", "weight": 600, "lineHeight": 1.1, "letterSpacing": "-0.02em" },
      "body": { "size": "17px", "weight": 400, "lineHeight": 1.6 },
      "small": { "size": "14px", "weight": 400, "lineHeight": 1.5 }
    },
    "hierarchy": "Extreme size jumps between headline and body. Headlines dominate the visual hierarchy."
  },
  "spacing": {
    "system": "8px base",
    "scale": [8, 16, 24, 32, 48, 64, 96, 128, 192],
    "containerMaxWidth": "1280px",
    "sectionPadding": "128px vertical on desktop, 64px on mobile",
    "componentSpacing": "24px between related elements",
    "gutters": "24px"
  },
  "components": {
    "buttons": {
      "primary": {
        "background": "linear-gradient(135deg, #667EEA 0%, #764BA2 100%)",
        "text": "#FFFFFF",
        "border": "none",
        "borderRadius": "8px",
        "padding": "14px 28px",
        "fontSize": "15px",
        "fontWeight": 500,
        "states": {
          "hover": "Brightness 110%, lift 2px with shadow",
          "active": "Scale 0.98",
          "disabled": "Opacity 0.5"
        },
        "shadow": "0 4px 14px rgba(102, 126, 234, 0.4)"
      }
    },
    "cards": {
      "style": "Flat with subtle border",
      "borderRadius": "12px",
      "padding": "32px",
      "shadow": "none",
      "border": "1px solid #27272A",
      "hoverEffect": "Border color to #3F3F46, subtle lift"
    }
  },
  "visualEffects": {
    "shadows": {
      "subtle": "0 1px 3px rgba(0,0,0,0.12)",
      "medium": "0 4px 14px rgba(0,0,0,0.25)",
      "button": "0 4px 14px rgba(102, 126, 234, 0.4)"
    },
    "gradients": [
      {
        "name": "Purple button gradient",
        "value": "linear-gradient(135deg, #667EEA 0%, #764BA2 100%)",
        "usage": "Primary CTAs"
      }
    ]
  },
  "animations": {
    "transitions": {
      "default": "all 0.2s cubic-bezier(0.4, 0, 0.2, 1)"
    },
    "microInteractions": [
      "Buttons lift 2px on hover with shadow increase",
      "Cards glow border on hover",
      "Smooth scroll reveals with fade-in"
    ]
  },
  "designPatterns": {
    "visualStyle": "Flat, minimal with strategic gradients",
    "aesthetic": "Ultra-modern, high-contrast, spacious",
    "keyCharacteristics": [
      "Massive headlines with tight letter-spacing",
      "High contrast black/white base",
      "Generous whitespace/negative space",
      "Subtle purple gradient accents",
      "Clean sans-serif typography only"
    ]
  }
}
```

**Vibe Coding Prompt**:
```
Create a modern SaaS landing page matching Linear's aesthetic:

**Overall Feel**: Ultra-minimal, high-contrast, spacious with subtle purple gradients

**Colors**:
- Background: Pure black #000000
- Text: White #FFFFFF primary, Gray #A1A1AA secondary
- Accent: Purple gradient (667EEA → 764BA2)
- Borders: Subtle dark gray #27272A

**Typography**:
- Font: Inter (weights 400, 500, 600)
- Hero headline: MASSIVE (96px), weight 600, line-height 1, tight -0.04em letter-spacing
- Body: 17px, weight 400, line-height 1.6
- Create extreme hierarchy through size contrast

**Layout**:
- Black hero section, full viewport height
- Centered content, max-width 1280px
- HUGE vertical spacing (128px between sections)
- Generous padding everywhere

**Components**:
- Primary button: Purple gradient background (667EEA → 764BA2), white text, 8px rounded, medium padding, purple glow shadow on hover, lifts 2px
- Cards: Dark background, 1px subtle border #27272A, 12px rounded, 32px padding, border glows on hover
- Text: High contrast white on black, gray for secondary info

**Effects**:
- Smooth transitions: 200ms cubic-bezier(0.4, 0, 0.2, 1)
- Purple gradient reserved for CTAs only
- Subtle shadows on interactive elements
- Clean, flat design (no neumorphism)

**Key Vibe Points**:
- Confidence through negative space
- Let typography do the heavy lifting
- Purple used sparingly for maximum impact
- Everything should feel fast and lightweight
```

### Example 2: Glassmorphic Dashboard

**Input**: "Extract design from this dashboard screenshot" [uploads image]

**Analysis Output**:
```
**Vibe**: Glassmorphic, modern, with backdrop blur and subtle transparency

**Color Palette**:
- Background gradient: #1A1A2E → #16213E
- Glass elements: rgba(255, 255, 255, 0.1) with backdrop blur
- Accent: #0F4C75 (Deep blue)
- Borders: rgba(255, 255, 255, 0.18)

**Key Design Elements**:
- Frosted glass cards with 20px backdrop blur
- Subtle white borders (18% opacity)
- Soft shadows: 0 8px 32px rgba(0, 0, 0, 0.37)
- 16px border radius throughout
- Gradient backgrounds for depth

**Typography**:
- Poppins font family
- White text with subtle opacity variations
- Size hierarchy: 32px / 24px / 16px / 14px

**Implementation Notes**:
- Use backdrop-filter: blur(20px) for glass effect
- Semi-transparent backgrounds
- Layer subtle gradients
- Keep borders minimal and subtle
```

## Extraction Workflow

### Step 1: Initial Assessment
```
1. Identify overall vibe and aesthetic category
2. Note primary purpose and target audience
3. Capture first impression and mood
```

### Step 2: Color Analysis
```
1. Extract all unique colors used
2. Identify color hierarchy (primary, secondary, accent)
3. Note color usage patterns
4. Check contrast ratios
5. Document gradients and overlays
```

### Step 3: Typography System
```
1. Identify all fonts used
2. Measure font sizes across headings and body
3. Note weights, line-heights, letter-spacing
4. Document hierarchy patterns
5. Check responsive scaling
```

### Step 4: Spacing & Layout
```
1. Measure spacing scale (4px, 8px, etc.)
2. Document section padding
3. Note container widths
4. Identify grid patterns
5. Check responsive breakpoints
```

### Step 5: Component Library
```
1. Extract button styles (all variants)
2. Document card patterns
3. Note form input styling
4. Capture navigation design
5. Identify unique components
```

### Step 6: Visual Effects
```
1. Document shadows (all levels)
2. Note border styles and radius
3. Extract gradients
4. Identify any blur/glass effects
5. Capture unique visual treatments
```

### Step 7: Animation & Interaction
```
1. Note transition timings
2. Document hover effects
3. Identify scroll animations
4. Capture micro-interactions
5. Note easing functions
```

## Vibe Coding Tool Optimization

### For v0.dev
```
Focus on: Component-first description, Tailwind classes, React patterns
Include: Specific color values, spacing scale, responsive breakpoints
Format: Structured with clear sections, component hierarchy
```

### For Bolt.new
```
Focus on: Full page context, layout structure, tech stack
Include: Color system, typography scale, component specifications
Format: Natural language with technical details
```

### For Lovable.dev
```
Focus on: Visual aesthetic, user experience, animation details
Include: Mood/vibe description, interaction patterns, visual effects
Format: Design-first language with implementation hints
```

### For Claude Artifacts
```
Focus on: Complete standalone components, inline styles if needed
Include: All styling in one place, clear structure
Format: Self-contained with full specifications
```

## Best Practices

### Color Extraction
- Use actual hex values from the page (browser devtools)
- Note opacity/alpha values for overlays
- Document gradient directions and stops
- Identify semantic color usage (success, error, etc.)

### Typography Analysis
- Measure computed font sizes (not relative units)
- Note actual rendered weights
- Check line-height in various contexts
- Document responsive scaling patterns

### Spacing Precision
- Use consistent measuring units
- Identify the base spacing unit (4px, 8px)
- Note exceptions to the spacing scale
- Document responsive spacing changes

### Component Detail
- Capture ALL states (default, hover, active, disabled, focus)
- Note transitions between states
- Document accessibility features
- Include responsive variations

### Animation Accuracy
- Time actual transitions (use devtools)
- Note easing functions
- Document trigger events
- Capture animation sequences

## Tips for Perfect Replication

1. **Start Broad, Then Detail**: Get the overall vibe first, then drill into specifics
2. **Use Actual Values**: Don't approximate - use actual measured values
3. **Document Context**: Note when/where elements are used
4. **Capture Edge Cases**: Unusual states, responsive behaviors
5. **Test Accuracy**: Compare your implementation side-by-side
6. **Iterate**: Refine based on visual comparison

## Common Design Vibes

**Minimal**: Lots of whitespace, limited color, simple typography, clean lines
**Brutalist**: Bold typography, harsh contrasts, asymmetric layouts, raw aesthetics
**Glassmorphic**: Transparent elements, backdrop blur, layered depth, subtle borders
**Neumorphic**: Soft shadows, subtle depth, monochromatic, tactile feel
**Gradient Heavy**: Vibrant gradients, colorful, energetic, modern
**Dark Mode**: Dark backgrounds, high contrast text, accent colors pop
**Corporate**: Professional, structured, blues/grays, formal typography
**Playful**: Bright colors, rounded corners, fun animations, casual fonts

## Output Customization

Request specific formats:
```
"Give me just the color palette"
"Extract only typography specs"
"Create a Tailwind config from this design"
"Generate CSS custom properties for this design system"
"What's the component library for this page?"
```

---

**Master the vibe.** Extract any design. Replicate perfectly. Ship beautiful products.
