# Design System Specification: The Brutalist Command

## 1. Overview & Creative North Star
**Creative North Star: "The Analog Architect"**
This design system moves beyond the cliché "neon-on-black" aesthetic to create a high-density, editorial-grade command center. It is inspired by the intentionality of mid-century mainframe terminals and the sharp, unforgiving precision of early glass-cockpit avionics. 

We are rejecting the "soft" web. There are no pill-shaped buttons, no soft blurs, and no organic curves. This is a system of absolute structure. The "editorial" feel is achieved through radical asymmetry—using large areas of dead space (Background: `#050505`) contrasted against dense clusters of technical data. The goal is to make the user feel like an operator, not a consumer.

---

## 2. Colors & Surface Architecture
The palette is hyper-limited to ensure every flash of color is a meaningful signal.

### The Palette
- **Primary (Cyan):** `#00FFFF` — Reserved for active data streams and interactive states.
- **Surface (Panel):** `#0A0A0A` — For primary structural containers.
- **Background:** `#050505` — The foundation of the viewport.
- **Error/Warning:** `#FF0000` / `#FFBF00` — High-visibility status indicators only.
- **Muted/Outline:** `#4B5563` — For non-critical metadata and inactive paths.

### The "No-Line" Rule
Standard 1px borders are strictly prohibited for layout sectioning. Boundaries between sections must be defined by background shifts. Use the `surface-container` tiers to create hierarchy:
- A `surface-container-low` (`#0A0A0A`) panel sits on the `background` (`#050505`).
- An inner card or focus area uses `surface-container-high` (`#2A2A2A`).
The lack of lines creates a more integrated, high-end "embedded" feel.

### Signature Texture: The CRT Overlay
To avoid a flat, "Bootstrap" appearance, the entire viewport must be covered by a global `CRT` overlay:
- **Scanlines:** A repeating linear pattern of 1px transparent black lines at 50% opacity.
- **Vignette:** A subtle radial falloff that darkens the extreme corners, focusing the operator’s eye on the central "Grid."
- **Chromatic Aberration:** A 1px red/cyan shift on hover states for primary interactive elements.

---

## 3. Typography: Data as Art
We utilize a **Strict Monospace** scale. In this system, text is not just content; it is a graphic element.

| Level | Size | Case | Tracking | Role |
| :--- | :--- | :--- | :--- | :--- |
| **Display** | 3.5rem | UPPER | -0.05em | Hero data points/System status |
| **Headline**| 1.5rem | UPPER | 0.1em | Section headers |
| **Title** | 1.125rem| Mixed | 0.0em | Component grouping |
| **Body-MD** | 0.875rem| Mixed | 0.0em | Narrative/Log data |
| **Label-SM**| 0.6875rem| UPPER | 0.2em | Metadata/Sub-labels |

**Editorial Direction:** Use `Label-SM` in `Muted Gray` for everything that isn't a direct action. When a header is used, it should be significantly larger than the body text to create a "Technical Manual" hierarchy.

---

## 4. Elevation & Depth: Tonal Layering
Traditional shadows are forbidden. Depth is achieved through **Tonal Stacking**.

- **The Stacking Principle:** To lift a component, move it one step up the surface-container scale. A `surface-container-highest` (`#353534`) element will naturally feel "closer" to the operator than the `background`.
- **The "Ghost Border" Fallback:** If a container requires a boundary for accessibility against a similar background, use the `outline-variant` token at **15% opacity**. This creates a "hairline" effect that suggests a boundary without creating a hard visual break.
- **Interference (Active Depth):** Instead of a shadow, an active or "floating" element should cause the CRT scanlines behind it to subtly shift or brighten, mimicking electronic interference.

---

## 5. Components

### Buttons
- **Primary:** Solid `#00FFFF` block with `#003737` text. 0px border radius.
- **Secondary:** Transparent background, `outline` `#00FFFF` border (1px), uppercase text.
- **Interaction:** On hover, the button should "flicker" (opacity shift from 100% to 80% rapidly) once. No smooth transitions; use `transition-duration: 0ms`.

### Inputs & Text Fields
- Forbid standard boxes. Use a "Terminal Prompt" style: a `surface-container-low` background with a 2px bottom-border of `Primary Cyan`.
- **Active State:** The bottom border pulses. The cursor is a solid cyan block (`width: 8px`).

### Cards & Lists
- **No Dividers:** Use the Spacing Scale (specifically `12` / `2.75rem`) to separate list items. 
- **Selection:** A selected list item changes its background to `surface-container-highest`.
- **Metadata:** All list items must include a `Label-SM` timestamp or ID code in the top-right corner to maintain the "System Log" aesthetic.

### Additional Component: "The Data Ribbon"
A 100% width, 24px high ticker bar at the top or bottom of panels. It displays scrolling system metrics in `Label-SM` cyan text. This reinforces the "real-time" nature of the dashboard.

---

## 6. Do's and Don'ts

### Do:
- **Embrace Density:** It is okay for the UI to look "busy" as long as it is organized on a strict grid.
- **Use Intentional Asymmetry:** If a panel is on the left, leave the right side of the screen as "Dead Space" (Background) to create an editorial, premium feel.
- **Align to the Pixel:** Since there are no rounded corners, alignment errors are glaring. Everything must snap to the `0.2rem` (Token 1) grid.

### Don't:
- **No Smoothing:** Do not use `antialiased` font rendering if possible; let the monospace look raw and digital.
- **No "Soft" Colors:** Avoid pastels or mid-tones. Stick to the high-contrast extremes of the provided palette.
- **No Animation Ease-in-out:** If something moves, it should be a linear step or an instant jump. Modern "fluid" animations break the retro-terminal immersion.

---
**Director's Note:** You are building a tool for power users. Treat the screen as a high-precision instrument. If it looks "friendly," you have failed. It should look powerful.