## Purpose
Provide concise, project-specific guidance so an AI coding agent is immediately productive on this repository: a small static single-page presentation site in Russian.

## Big picture
- **Type**: Static single-page site (HTML + CSS + vanilla JS). Key files: [index.htm](../index.htm), [script.js](../script.js), [styles.css](../styles.css), images in [img/](../img/).
- **Runtime flow**: `index.htm` renders 10 slides sequentially; `script.js` controls slide state via `currentSlide`, `showSlide(n)`, `nextSlide()`, `prevSlide()` and adds keyboard handlers (Arrow Left/Right). There is no backend or build step.

## What to edit and how
- **Add or modify slides**: replicate the structure used in [index.htm](../index.htm) — each slide is a `div` with classes `slide slide-N` (order in DOM determines index). The JS expects a plain NodeList of `.slide` elements and uses positional indexes, so keep slide order stable.
- **Styling approach**: Heavy use of inline styles for gradients, spacing, and colors. When modifying slides, match existing inline style patterns (e.g., `background: linear-gradient(135deg, ...)`). Each slide has unique background gradients defined via `.slide-N` classes in [styles.css](../styles.css).
- **Navigation**: `script.js` binds to elements with IDs `prevBtn` and `nextBtn`. The nav buttons are absolutely positioned at bottom center with z-index 20. Do not rename these IDs unless you update the selectors and their event bindings.
- **Animations**: `showSlide(n)` toggles `active`, `next`, `prev` classes — follow this pattern for CSS transitions. Direction detection (forward/backward) creates smooth slide animations.

## Developer workflows (no build system)
- To preview locally run a lightweight static server. Examples (works in PowerShell on Windows):

```bash
python -m http.server 8000
# or with Node if installed
npx http-server -p 8000
```

- Alternatively use VSCode Live Server extension and open [index.htm](../index.htm).

## Project-specific conventions & gotchas
- **Files and content are in Russian**; ensure UTF-8 encoding is preserved when editing files.
- **Repository root path contains non-Latin characters** — some tools or linters may mis-handle paths; prefer editors that handle Unicode paths (VS Code does).
- **Minimal DOM assumptions**: `script.js` expects a flat set of `.slide` elements; adding nested wrappers or changing ordering can break slide indexing.
- **Inline styles are heavily used** in slide elements for layout/decoration (e.g., gradient backgrounds, specific padding/margins, emoji placement). When changing styling prefer updating [styles.css](../styles.css) for global changes, but preserve inline styles for slide-specific designs.
- **Mobile responsiveness**: Extensive mobile-specific CSS in media query `@media (max-width: 768px)` with per-slide overrides. When modifying slides, test mobile view and update corresponding mobile CSS rules if needed.
- **Slide numbering**: Each slide has a `.slide-number` div positioned absolutely at bottom center showing the slide number (1-10).
- **Decorative elements**: `.decoration`, `.decoration-star`, `.decoration-book` elements provide visual flair; they're positioned absolutely with low opacity and don't affect layout.

## Integration points & dependencies
- No external services or package dependencies. Images live in `img/` (example: `img/qr_Elib_site.png`).

## Examples
- Add a new slide: copy a `div.slide` block from [index.htm](../index.htm) and insert it where you want it to appear; `script.js` will pick it up automatically.
- Hook additional buttons: query the element and call `nextSlide()` / `prevSlide()` — maintain the same animation class pattern.

## What not to change lightly
- Avoid renaming `prevBtn`, `nextBtn`, `.slide` classes, or altering the numeric ordering behavior without updating `script.js`.

## Questions for maintainers
- Should we add a simple local test harness (e.g., Cypress/playwright) or keep the repo intentionally dependency-free?

---
If anything is unclear or you want more examples (e.g., how to add an ARIA-friendly slide), tell me which part to expand.
