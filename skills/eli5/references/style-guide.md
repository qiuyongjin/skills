---
name: eli5-style-guide
description: Visual and voice standards for eli5 HTML artifacts. Use when generating or reviewing any eli5 output.
---

# eli5 Visual & Voice Style Guide

This guide is the source of truth for every eli5 HTML artifact. Apply it without exception. Following it is what makes outputs recognizably "eli5".

## Palette

Use only these tokens. Reference them by name in your CSS variables.

| Token   | Hex       | Use                                       |
|---------|-----------|-------------------------------------------|
| `paper` | `#FFF8E7` | Page background                           |
| `sun`   | `#FFE5B4` | Warm accents, primary fills               |
| `blush` | `#FFB6C1` | Secondary accents, hearts, highlights     |
| `sky`   | `#87CEEB` | Cool elements, water, sky, links          |
| `cloud` | `#F5F5F5` | Card and panel backgrounds                |
| `leaf`  | `#A8D5A2` | Optional nature accents (use sparingly)   |
| `ink`   | `#2D2D2D` | Text, outlines, strokes                   |

```css
:root {
  --paper: #FFF8E7;
  --sun:   #FFE5B4;
  --blush: #FFB6C1;
  --sky:   #87CEEB;
  --cloud: #F5F5F5;
  --leaf:  #A8D5A2;
  --ink:   #2D2D2D;
}
```

Do not introduce additional colors. If a topic needs a color outside this palette, reuse the closest token.

## Typography

| Role    | Family       | Weight | Source        |
|---------|--------------|--------|---------------|
| Display | Caveat       | 700    | Google Fonts  |
| Body    | Comic Neue   | 400/700 | Google Fonts |
| Mono    | ui-monospace | 400    | system        |

```css
@import url('https://fonts.googleapis.com/css2?family=Caveat:wght@700&family=Comic+Neue:wght@400;700&display=swap');

:root {
  --font-display: 'Caveat', cursive;
  --font-body:    'Comic Neue', system-ui, sans-serif;
}

body {
  font-family: var(--font-body);
  font-size: 1.1rem;
  line-height: 1.6;
  max-width: 65ch;
  margin: 0 auto;
  padding: 2rem 1.5rem;
  background: var(--paper);
  color: var(--ink);
}

.title   { font-family: var(--font-display); font-size: clamp(2.5rem, 6vw, 4.5rem); line-height: 1.1; margin: 0 0 1rem; }
.heading { font-family: var(--font-display); font-size: clamp(1.5rem, 3.5vw, 2.25rem); line-height: 1.2; margin: 2rem 0 0.5rem; }
.caption { font-family: var(--font-body);    font-size: 1rem; color: var(--ink); opacity: 0.7; }
```

## Illustration rules

All illustrations are inline SVG. No external image files. No AI-generated raster images.

- Stroke width: `3` for main outlines, `2` for details.
- `stroke-linecap="round"` and `stroke-linejoin="round"` on every path.
- Corner radius: `8` on rectangles and panel borders.
- Maximum 6 elements per scene — keep compositions simple and readable.
- Faces: two dots for eyes, one short curve for a smile. No realistic faces.
- Bodies: simple geometric primitives (circles, rounded rectangles).
- Do not use: gradients, drop shadows, blur filters, opacity below 0.8, raster textures.

## Layout primitives

Compose the page from these three patterns. Use one, two, or all three — order is up to the topic.

### Card

A rounded panel for grouping one idea.

```html
<article class="card">
  <svg viewBox="0 0 200 120" aria-hidden="true">{illustration}</svg>
  <p>One idea, one sentence.</p>
</article>
```

```css
.card {
  background: var(--cloud);
  border: 2px solid var(--ink);
  border-radius: 16px;
  padding: 1.5rem 2rem;
  margin: 1.5rem 0;
}
.card svg { width: 100%; max-width: 320px; height: auto; margin: 0 auto 1rem; display: block; }
```

### Side-by-side

Two cards in a row for comparison ("A vs B"). Collapses to a single column on narrow screens.

```html
<div class="row">
  <article class="card">{A}</article>
  <article class="card">{B}</article>
</div>
```

```css
.row { display: grid; grid-template-columns: 1fr 1fr; gap: 1.5rem; }
@media (max-width: 640px) { .row { grid-template-columns: 1fr; } }
```

### Timeline

3–5 circles connected by a dashed line, for sequences or processes.

```html
<div class="timeline">
  <span class="step">1</span>
  <span class="step">2</span>
  <span class="step">3</span>
</div>
```

```css
.timeline { display: flex; align-items: center; gap: 1rem; flex-wrap: wrap; margin: 1.5rem 0; }
.timeline .step {
  width: 56px; height: 56px;
  border-radius: 50%;
  background: var(--sun);
  border: 2px solid var(--ink);
  display: grid; place-items: center;
  font-family: var(--font-display); font-size: 1.75rem;
}
.timeline .step:not(:last-child)::after {
  content: "→";
  margin-left: 1rem;
  font-size: 1.5rem;
  color: var(--ink);
}
```

## Reusable icons

Copy these SVG snippets verbatim. They establish the visual rhythm across artifacts.

```html
<!-- sun -->
<svg viewBox="0 0 64 64" fill="none" stroke="#2D2D2D" stroke-width="3" stroke-linecap="round" stroke-linejoin="round">
  <circle cx="32" cy="32" r="12" fill="#FFE5B4"/>
  <line x1="32" y1="6"  x2="32" y2="14"/>
  <line x1="32" y1="50" x2="32" y2="58"/>
  <line x1="6"  y1="32" x2="14" y2="32"/>
  <line x1="50" y1="32" x2="58" y2="32"/>
  <line x1="13" y1="13" x2="19" y2="19"/>
  <line x1="45" y1="45" x2="51" y2="51"/>
  <line x1="13" y1="51" x2="19" y2="45"/>
  <line x1="45" y1="19" x2="51" y2="13"/>
</svg>

<!-- cloud -->
<svg viewBox="0 0 64 64" fill="#F5F5F5" stroke="#2D2D2D" stroke-width="3" stroke-linecap="round" stroke-linejoin="round">
  <path d="M16 44 Q10 44 10 38 Q10 32 16 32 Q16 22 26 22 Q36 22 36 32 Q44 32 44 38 Q44 44 38 44 Z"/>
</svg>

<!-- raindrop -->
<svg viewBox="0 0 64 64" fill="#87CEEB" stroke="#2D2D2D" stroke-width="3" stroke-linecap="round" stroke-linejoin="round">
  <path d="M32 8 Q20 28 20 40 Q20 52 32 52 Q44 52 44 40 Q44 28 32 8 Z"/>
</svg>

<!-- person -->
<svg viewBox="0 0 64 64" fill="none" stroke="#2D2D2D" stroke-width="3" stroke-linecap="round" stroke-linejoin="round">
  <circle cx="32" cy="20" r="8" fill="#FFE5B4"/>
  <path d="M16 56 Q16 38 32 38 Q48 38 48 56" fill="#FFB6C1"/>
</svg>

<!-- arrow -->
<svg viewBox="0 0 64 64" fill="none" stroke="#2D2D2D" stroke-width="3" stroke-linecap="round" stroke-linejoin="round">
  <line x1="8" y1="32" x2="56" y2="32"/>
  <polyline points="44 20 56 32 44 44"/>
</svg>

<!-- box -->
<svg viewBox="0 0 64 64" fill="#FFE5B4" stroke="#2D2D2D" stroke-width="3" stroke-linecap="round" stroke-linejoin="round">
  <rect x="12" y="20" width="40" height="32" rx="4"/>
  <line x1="12" y1="32" x2="52" y2="32"/>
</svg>

<!-- eye -->
<svg viewBox="0 0 64 64" fill="#FFFFFF" stroke="#2D2D2D" stroke-width="3" stroke-linecap="round" stroke-linejoin="round">
  <path d="M8 32 Q32 12 56 32 Q32 52 8 32 Z"/>
  <circle cx="32" cy="32" r="6" fill="#2D2D2D"/>
</svg>

<!-- hand -->
<svg viewBox="0 0 64 64" fill="#FFE5B4" stroke="#2D2D2D" stroke-width="3" stroke-linecap="round" stroke-linejoin="round">
  <path d="M20 50 L20 24 Q20 18 26 18 Q26 18 26 24 L26 14 Q26 8 32 8 Q38 8 38 14 L38 24 Q38 18 44 18 Q50 18 50 24 L50 50 Q50 58 42 58 L28 58 Q20 58 20 50 Z"/>
</svg>

<!-- heart -->
<svg viewBox="0 0 64 64" fill="#FFB6C1" stroke="#2D2D2D" stroke-width="3" stroke-linecap="round" stroke-linejoin="round">
  <path d="M32 56 Q8 40 8 24 Q8 12 20 12 Q28 12 32 20 Q36 12 44 12 Q56 12 56 24 Q56 40 32 56 Z"/>
</svg>

<!-- lightbulb -->
<svg viewBox="0 0 64 64" fill="#FFE5B4" stroke="#2D2D2D" stroke-width="3" stroke-linecap="round" stroke-linejoin="round">
  <path d="M20 28 Q20 14 32 14 Q44 14 44 28 Q44 36 38 40 L38 48 L26 48 L26 40 Q20 36 20 28 Z"/>
  <line x1="26" y1="54" x2="38" y2="54"/>
  <line x1="28" y1="58" x2="36" y2="58"/>
</svg>
```

## Voice

Write like you're explaining to a curious 5-year-old sitting next to you.

- One idea per sentence. Short sentences (≤ 14 words).
- Use the word order a child would use. "The sun makes light" beats "Light is emitted by the sun."
- Concrete before abstract. "Water drops in the sky" before "condensation."
- Use daily-life analogies. "Like when you spill juice on the table and it spreads out…"
- Define new words right after using them. "Refraction means light bending when it goes through water."
- Never use jargon without a translation. If a word feels grown-up, replace it.
- End each artifact with one line that ties the topic to wonder. "And that's why every drop of rain holds a tiny rainbow!"

## Anti-patterns

Avoid these — they break the visual identity.

- Different fonts per artifact. Always Caveat + Comic Neue.
- Drop shadows, gradients, blur filters.
- Realistic faces, detailed anatomy, or photographic imagery.
- More than 3 distinct hues in one illustration.
- Long paragraphs (more than 3 sentences) — break them up.
- Mixed art styles: one panel pixel-art, another watercolor, another flat.
- Tailwind, Bootstrap, or any CSS framework. Hand-written CSS only.
- Dark mode variants. The light palette is the brand.