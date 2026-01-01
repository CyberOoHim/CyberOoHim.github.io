# Experience Log: Black Bear Favicon Dark Mode Visibility

## Problem Description

The project introduced a custom "Black Bear" SVG as the primary favicon and logo. During the transition to dark mode support, a common issue was identified:

1. **Invisibility**: On a dark background, a pure black SVG becomes invisible.
2. **Color Inversion**: Standard CSS filters like `dark:invert` (100% inversion) solve the visibility problem but turn the bear into a "Pure White Bear," which loses the brand's identity and visual weight.

## Design Goal

Maintain the bear as a **Black Bear** across all themes while ensuring it remains clearly visible and distinct against dark backgrounds.

## SVG Source Code ("Asset")

The following SVG defines the brand asset:

```svg
<svg width="500" height="500" viewBox="0 0 500 500" xmlns="http://www.w3.org/2000/svg">
  <g fill="#000000">
    <circle cx="165" cy="180" r="40" />
    <circle cx="335" cy="180" r="40" />
    <path d="M 150 210 Q 250 150 350 210 C 410 240 430 350 440 420 Q 445 480 250 480 Q 55 480 60 420 C 70 350 90 240 150 210 Z" />
  </g>
  <path d="M 105 305 L 250 400 L 395 305 L 410 305 L 250 450 L 90 305 Z" fill="#FFFFFF" />
  <g>
    <circle cx="205" cy="245" r="16" fill="#FFFFFF" />
    <circle cx="205" cy="245" r="7" fill="#000000" />
    <circle cx="295" cy="245" r="16" fill="#FFFFFF" />
    <circle cx="295" cy="245" r="7" fill="#000000" />
  </g>
  <path d="M 220 280 Q 250 260 280 280 Q 295 310 280 330 Q 250 345 220 330 Q 205 310 220 280 Z" fill="#FFFFFF" />
  <path d="M 235 285 Q 250 280 265 285 Q 270 295 250 310 Q 230 295 235 285 Z" fill="#000000" />
  <rect x="248" y="310" width="4" height="10" rx="2" fill="#000000" />
</svg>
```

## Color Reference ("Tickets")

The following colors define the environment and the solution:

| Element | Color Ticket | Usage |
| :--- | :--- | :--- |
| **Light BG** | `#FAFAFA` | `background-light` (Tailwind) |
| **Dark BG** | `#0F1115` | `background-dark` (Tailwind) |
| **Shadow High** | `rgba(255, 255, 255, 0.9)` | 1px Outline Glow |
| **Shadow Soft** | `rgba(255, 255, 255, 0.6)` | 2px Ambient Glow |

## Implementation Details

### The "Outline" vs "Invert" Approach

Instead of inverting the colors of the SVG itself, we implemented a **Halo/Outline strategy** using CSS `drop-shadow` filters. This allows the inner content (the black bear) to remain black while creating a luminous silhouette.

### Visual Refinements

To ensure the logo sits perfectly adjacent to the text:

1. **Size**: Increased to **40px** (up from 32px) to better match the visual weight of the header text.
2. **Alignment**: Used `margin-bottom: 6px` on the logo. This "lifts" the logo visually so its bottom aligns flush with the text baseline, compensating for the text's line-height/descender space.

### Cyberpunk "Glitch" Styling (Final)

To align with a more modern, edgy aesthetic, we evolved the visibility strategy from a simple white outline to a **Chromatic Aberration (Glitch)** effect.

### Technical Implementation

In `assets/css/styles.css`, we implemented the effects using standard CSS `filter: drop-shadow`:

#### Light Mode (Base)

High-contrast, solid offsets for a crisp "print error" look.

```css
.site-logo {
    /* ... size & alignment ... */
    filter: drop-shadow(-2px 0 0 #32cd32) drop-shadow(2px 0 0 #ff6347);
}
```

#### Dark Mode (Dimmer Glitch)

Initial tests showed that solid colors were too distracting in dark mode. We refined the intensity by **dimming** the effect:

* **Translucent Offsets**: Reduced opacity to 50% (`0.5`) so the glitch doesn't overpower the logo.
* **Subtle Glow**: Added a third shadow layer (`0 0 5px`) at 15% opacity to simulate a faint CRT screen glow without reducing legibility.

```css
@media (prefers-color-scheme: dark) {
    .site-logo {
        filter: drop-shadow(-2px 0 0 rgba(50, 205, 50, 0.5)) 
                drop-shadow(2px 0 0 rgba(255, 99, 71, 0.5)) 
                drop-shadow(0 0 5px rgba(50, 205, 50, 0.15));
    }
}
```

### Why Glitch over Glow?

The glitch effect provides high contrast borders (green/orange) against both white and black backgrounds while adding unique character ("cyberpunk/tech") that a simple white halo lacks.

## Outcome

* **Identity Preserved**: The bear remains black, maintaining brand consistency.

* **Accessibility**: The logo is clearly visible on both light and dark backgrounds.
* **Visual Appeal**: The subtle white glow provides a premium, "backlit" feel in dark mode without the harshness of a pure white inversion.

## Lessons Learned

When dealing with dark-colored iconography in dark mode, **silhouette-enhancement** (shadows/outlines) is often superior to **color-inversion** if the color itself carries semantic or brand meaning.
