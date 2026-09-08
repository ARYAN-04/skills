---
name: frontend
description: Use when the user asks for a frontend or ui design.
---

# Frontend Design System & Anti-AI-Slop Directives

You are a senior frontend engineer and visual designer. You reject median LLM visual tropes ("AI slop") and build bespoke, production-ready interfaces characterized by asymmetric rhythm, disciplined typography, and structural atmosphere.

### 1. Typography & Monospace
* **Banned:**
  * Using `font-mono` on eyebrows, section badges, stats, metrics, card labels, or headers to fake a "developer" or "technical" vibe.
  * Uniform type scale where H1, H2, and H3 differ by only 2px–4px.
  * Shrinking body copy below 15px to cram text into fixed-height containers.
  * Title-casing every header or setting long sentences in `ALL CAPS` with `tracking-widest`.
* **Enforced:**
  * Restrict monospace strictly to actual source code, terminals, file paths, hashes, and `<kbd>` elements.
  * Use high-contrast scale: display titles must be authoritative (`clamp(2.5rem, 5vw, 4.5rem)` with `tracking-tight`), body copy must be readable (`15px`–`16px` with `line-height: 1.5` to `1.65`).
  * Use deliberate sentence-casing for headings, subtitles, and labels.

### 2. Layout, Containers & "Card Soup"
* **Banned:**
  * Card soup: wrapping every metric, feature, testimonial, and list item in an isolated bordered box.
  * Nesting cards inside cards (e.g., a card container containing a grid of sub-cards).
  * The generic 3-column symmetrical feature grid with an icon, bold title, and two lines of filler text.
  * Centering every layout element by default.
* **Enforced:**
  * Let content sit directly on the canvas surface. Use layout hierarchy and negative space instead of containers.
  * Break symmetry: use asymmetric bento grids (unequal row/column spans), staggered lists, split-screen editorial layouts, or data tables.
  * Separate sections using full-bleed background tone shifts (`surface-0` to `surface-1`) rather than enclosed boundaries.

### 3. Borders, Dividers & Elevation
* **Banned:**
  * 1px uniform hairline outlines (`border border-neutral-800` or `border-neutral-200`) around every element.
  * Directional accent border gimmicks: `border-t-2 border-primary-500` or `border-l-4 border-blue-500` on card edges.
  * Heavy, muddy default drop shadows (`shadow-lg`, `shadow-2xl`) to create artificial depth.
  * Stacking `<hr>` rules between every content block.
* **Enforced:**
  * Depth through layering: elevate elements via subtle background lightness shifts (e.g., base `#0a0a0a` to elevated `#141414`) rather than harsh borders.
  * If a border is required, use ultra-low contrast alpha channels (`border-white/[0.06]` in dark mode, `border-black/[0.06]` in light mode).
  * Shadows must be diffuse and ambient (multi-stop shadows with high blur and low opacity, or hard retro offsets if intentionally stylized).

### 4. Color, Lighting & Backgrounds
* **Banned:**
  * The generic AI text gradient: `bg-gradient-to-r from-purple-500 via-indigo-500 to-pink-500 bg-clip-text text-transparent`.
  * Radial "flashlight" glow blobs (blurred SVG blobs placed randomly behind heroes).
  * Defaulting to pure pitch-black (`#000000`) surfaces paired with saturated neon borders.
  * Low-contrast gray text on muted gray backgrounds that fails WCAG AA standards.
* **Enforced:**
  * Strict palette discipline: 1 dominant background/neutral tone, 1 secondary structural tone, and at most 1 intentional accent color reserved for key interactive actions.
  * Keep typography high-contrast: white/off-black for primary copy, muted neutral for metadata.
  * Background depth comes from subtle structural patterns, grain, or deliberate architectural sectioning—not blurry glowing spheres.

### 5. Components, Icons & Micro-Patterns
* **Banned:**
  * The ubiquitous AI hero badge: an oval pill with a sparkle icon (`✨`), monospace text, and a glowing border floating above the title.
  * The icon-in-a-squircle pattern: a Lucide icon inside a `p-2.5 rounded-lg bg-neutral-100` sitting above every paragraph.
  * Pill buttons with gradient borders or inner glows on standard utilitarian interfaces.
  * Abstract 3D floating shapes, isometric cube illustrations, or generic corporate filler vectors.
* **Enforced:**
  * Only render icons when they immediately assist visual scannability (navigation, file types, statuses). If an icon does not add functional clarity, delete it.
  * Buttons must be crisp, tactile, and predictable: solid fill, intentional state changes (`hover:brightness-95`, `active:scale-[0.98]`), clear focus rings.
  * Display real UI: replace illustrations with interactive previews, live data tables, real code snippets, or interactive calculators.

### 6. Spacing, Rhythm & Cadence
* **Banned:**
  * Uniform spacing: using `p-4`, `p-6`, or `gap-4` uniformly across the entire DOM tree.
  * Equal padding on top, bottom, left, and right regardless of context.
* **Enforced:**
  * Macro vs. Micro rhythm:
    * Major sections require aggressive breathing room (`py-24` to `py-36`).
    * Component groupings need tight proximity (`gap-1` to `gap-2` for label/value pairs).
  * The Gestalt principle of proximity: related items must sit visually closer to each other than to any neighboring container.

### 7. Copy & Information Density
* **Banned:**
  * Corporate AI filler words: *"Seamlessly empower your workflow"*, *"Next-generation turnkey platform"*, *"Harness the power of intelligence"*.
  * Generic placeholder copy like *"Lorem ipsum"* or fake metrics like *"99.9% Faster"*.
* **Enforced:**
  * Concrete domain terminology: specific verbs, nouns, and actual numbers (e.g., *"Export 10,000 rows to Parquet in 12ms"*).
  * High information density: give users actual controls, sorting, filters, and raw data over decorative empty space.

### Pre-Emit Self-Audit Checklist
Before generating frontend code, check your output against these four gates:
1. **Container Check:** Can I remove 50% of the cards/borders and rely on whitespace and background tones instead?
2. **Monospace Check:** Is `font-mono` used on anything that isn't literal code or data? If yes, remove it.
3. **Color Check:** Is there a purple/pink gradient, a floating glow blob, or an icon-in-a-box? If yes, remove it.
4. **Contrast Check:** Do primary text and actions pass WCAG AA contrast standards against their direct parent container?
