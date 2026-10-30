# Refactoring UI — Key Insights

**Central philosophy:** Design with tactics, not talent. Replace vague artistic instinct with a concrete, repeatable toolkit.

---

## Start with Features, Not Layouts

An app is a collection of features, not a shell. Don't start by asking "should it have a sidebar?" — start with a specific piece of functionality (like "search for a flight") and the UI elements you need will become obvious. Designing in the abstract leads to paralysis.

---

## Work Low-Fidelity First

Don't obsess over colors, typefaces, or shadows early on. Sketch with a Sharpie — it makes it physically impossible to fuss over details. Design in grayscale first, so you're forced to rely on spacing, contrast, and size to establish structure before layering on visual polish. Ship the smallest useful version, then iterate.

---

## Visual Hierarchy Is Everything

The most emphasized principle in the book. Hierarchy is what makes an interface feel *designed* rather than like a random pile of elements. The tools:

- **Size** — signal importance, but don't overdo it (headings don't need to be massive)
- **Weight** — bold text draws the eye more than changing font size
- **Color & contrast** — dark for primary content, grey for secondary, lighter grey for tertiary
- **Placement** — de-emphasize surrounding elements to let the primary one stand out

Action buttons follow the same logic: primary actions get solid, high-contrast backgrounds; secondary actions get outlines or muted colors; destructive actions shouldn't be big and red unless they're the *primary* action on that page.

---

## Systematize Your Design Decisions

Design systems prevent decision fatigue by constraining choices upfront. Define scales for font sizes, spacing, colors, shadows, and border radii *before* designing screens. Systematize everything: font size, weight, line height, color, margin, padding, width, height, box shadows, border radius, border width, opacity. Build a spacing scale from a base value (e.g. 16px) using consistent multipliers.

---

## Build a Real Color Palette

Forget five-hex-code palette generators. A real UI palette needs:

- **1–2 primary colors** with 5–10 shades each (buttons, active navigation, brand identity)
- **8–10 shades of grey** (text, backgrounds, panels, form controls)
- **3–4 accent colors** with multiple shades (error, warning, success, info states)

Start with a middle shade, define the darkest and lightest extremes, then fill in the gaps. Greys don't have to be pure grey — a touch of blue makes them feel cool; yellow or orange makes them warm.

---

## Typography Matters More Than You Think

- Use a scale of ~11 font sizes (from ~12px to ~72px), with smaller jumps at the bottom and larger jumps at the top
- Use fonts with at least five weights — they tend to be more carefully crafted
- Keep line length between 45–75 characters per line for readability
- Line height and font size are inversely proportional: small text needs more line spacing, large text needs less
- Align text by baseline when mixing font sizes; right-align numbers in tables

---

## Use Shadows and Depth Intentionally

- **Small, tight shadows** → element sits close to the surface (buttons)
- **Large, blurry shadows** → element is elevated toward the user (modals, dropdowns)
- Use two-part shadows for more realistic results: a soft, large ambient shadow + a tighter, darker direct shadow
- Even flat designs can convey depth through lighter/darker shades of the same color, overlapping elements, or zero-blur offset shadows

---

## Spacing: Start with Too Much

Cramped designs are the most common mistake. Start with more white space than you think you need, then tighten. Avoid ambiguous spacing: the space *around* a group of elements should always be greater than the space *within* it, so grouping relationships stay clear.

---

## Don't Rely on Color Alone

Always use color to support what your design is already communicating — never as the sole signal. Add + and − signs alongside trend colors, use contrast between shades in charts rather than entirely different hues, and make sure designs hold up for color-blind users.

---

## The Finishing Touches

Small tweaks that elevate an otherwise flat UI:

- Replace bullet points with icons; use custom checkboxes and radio buttons in brand colors
- Add accent borders (top of cards, side of alerts) for personality
- Use fewer borders — prefer box shadows, different backgrounds, or extra spacing to create separation
- Design empty states intentionally: illustrations, clear calls to action, not a blank screen
- Reimagine default UI patterns: dropdowns as multi-column sections, radio buttons as selectable cards, tables with combined data and images
