# Comprehensive Design System: CIPS 2026 Revision Hub

## 1. Overview & Creative North Star
This design system is anchored by the Creative North Star: **"The Academic Luminary."** 

To move beyond the utilitarian aesthetics of standard educational apps, this system treats the CIPS revision process as a premium editorial experience. It eschews the rigid, "boxed-in" feel of traditional Material Design in favor of **Organic Layering**. By utilizing intentional asymmetry, expansive negative space, and a high-contrast typographic hierarchy, we transform a functional revision tool into an authoritative digital environment. The goal is to make the user feel they are engaging with a high-end publication rather than just a database of questions.

---

## 2. Color & Tonal Architecture
The palette is a sophisticated interplay between the authority of `cips-navy` and the digital vitality of `cips-cyan`, set against a breathable foundation of `cips-ice`.

### The "No-Line" Rule
To achieve a high-end editorial feel, designers are **prohibited from using 1px solid borders** for sectioning or container definition. Boundaries must be defined strictly through:
*   **Background Shifts:** Placing a `surface-container-lowest` card on a `surface-container-low` background.
*   **Tonal Transitions:** Using the subtle difference between `surface` (#faf8ff) and `surface-variant` (#dae2fd) to guide the eye.

### Surface Hierarchy & Nesting
This system treats the mobile screen as a series of physical layers. We use the surface-container tiers to create nested depth:
*   **Base Layer:** `surface` (#faf8ff) – The ultimate canvas.
*   **Content Sections:** `surface-container-low` (#f2f3ff) – Used to group related modules.
*   **Interactive Cards:** `surface-container-lowest` (#ffffff) – Reserved for the most important interactive elements to provide a "natural lift."

### The "Glass & Gradient" Rule
To elevate the UI beyond a standard "flat" look:
*   **Glassmorphism:** Navigation bars and floating action elements should utilize `surface` colors at 85% opacity with a `backdrop-blur` effect (20px-30px). This ensures the layout feels integrated and breathable.
*   **Signature Textures:** Use a subtle linear gradient (from `secondary` #00687a to `secondary_container` #57dffe) for primary action buttons and progress indicators to inject a sense of "visual soul."

---

## 3. Typography: The Editorial Voice
We use **Inter** not just for legibility, but as a branding tool. The contrast between bold, oversized headlines and refined, spaced-out body text creates an authoritative, magazine-like rhythm.

*   **Display (lg/md):** Used for "Hero" moments, such as module titles or quiz scores. These should be bold with a slight negative letter-spacing (-0.02em).
*   **Headlines:** Your primary navigational anchors. Use `headline-sm` (1.5rem) for section headers to establish a clear vertical rhythm.
*   **Body (lg/md):** Set in `on_surface_variant` (#45464d) for long-form reading to reduce eye strain.
*   **Labels:** Always uppercase with increased letter-spacing (+0.05em) when used for category tags or metadata.

---

## 4. Elevation & Depth
In this system, depth is a product of light and layering, not artificial structure.

*   **Tonal Layering:** Avoid shadows for static cards. Instead, stack `surface-container-lowest` on `surface-container-high`. This mimics the look of fine paper stock layered on a desk.
*   **Ambient Shadows:** For floating elements (like the Bottom Nav), use an "Ambient Light" shadow: `box-shadow: 0 12px 32px rgba(15, 23, 42, 0.06);`. The shadow color must be a tinted version of `on-surface` (#131b2e) rather than pure black.
*   **The "Ghost Border" Fallback:** If a container requires further definition (e.g., a quiz input), use a **Ghost Border**: `outline-variant` (#c6c6cd) at 15% opacity. High-contrast, 100% opaque borders are strictly forbidden.

---

## 5. Components

### Interactive Cards
Cards are the heart of the revision hub. Use a `xl` (1.5rem) corner radius for main module cards.
*   **Styling:** No borders. Use `surface-container-lowest` with an ambient shadow on hover/press.
*   **Content:** Forbid divider lines. Use vertical spacing (1.5rem to 2rem) to separate the title from the progress bar.

### Buttons (Primary & Secondary)
*   **Primary:** A gradient-fill using `secondary` tokens. Pill-shaped (`full` roundedness) to contrast against the softer `xl` card corners.
*   **Tertiary:** Text-only with an icon. Avoid the "box" look to keep the interface light.

### Mobile Navigation (Bottom Nav)
*   **Style:** A glassmorphic bar (85% `surface_container_lowest`) floating 16px from the bottom edge.
*   **Active State:** Use a `cips-cyan` (#06b6d4) dot or subtle underline rather than a filled container.

### Accessible Quiz Elements
*   **Input Fields:** Ghost borders only. When focused, the border transitions to a 2px `secondary` (#00687a) stroke to ensure Android 8.1 accessibility compliance.
*   **Checkboxes/Radios:** Use `secondary` for selected states. Ensure the touch target is a minimum of 48x48dp.

---

## 6. Do's and Don'ts

### Do
*   **DO** use whitespace as a functional tool to group content. If elements feel cluttered, increase the padding—don't add a line.
*   **DO** use the `display-lg` typography for success states (e.g., "Module Complete!") to create a celebratory editorial moment.
*   **DO** ensure all text maintains a 4.5:1 contrast ratio against background surfaces for WCAG AA compliance.

### Don't
*   **DON'T** use 100% opaque shadows. They feel "heavy" and dated. Stick to the 4%-8% opacity range.
*   **DON'T** use standard Android "Dividers." Use a 8dp or 16dp gap of `surface-container-low` color to create separation.
*   **DON'T** mix corner radii. Stick to `xl` (1.5rem) for containers and `full` for buttons/chips to maintain a consistent visual language.