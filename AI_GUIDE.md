# AI guide: making study-visuals pages

Instructions for any AI assistant (Claude, ChatGPT/Codex, Gemini, ...) that adds or edits pages in this repo. Read all of it before writing a page.

## What this repo is

Interactive, step-by-step diagrams for the owner's university course notes. Each page explains one idea that is hard to follow from text alone (pointer changes, loops, algorithms). Pages are deployed by Vercel and embedded in Obsidian notes with an iframe, so that the written notes can stay short.

- Live site: https://study-visuals-five.vercel.app
- Every push to `main` redeploys automatically (about 30 seconds). No build step.

## When to make a page

Make one when a topic's scenario or logic is complex: something easier to understand by watching it change step by step. Do not make pages for simple definitions.

## Workflow

1. Copy `_template/stepper.html` to `<course-folder>/<concept>.html`.
   - Course folder: course code in lowercase, e.g. `cst108/` (CST108 Programming Practice).
   - File name: kebab-case, e.g. `insert-at-end.html`.
2. Fill in the header, the code panel, the steps, the drawing and the key points (see "Content" below).
3. Add the page to the `courses` array in `index.html` (create a new course entry if needed, with code and full course name).
4. Check it (see "Checklist").
5. Commit and push to `main`. If you cannot push, give the owner the complete file(s) and say where they go.
6. Give the owner the Obsidian embed code:

   ```html
   <iframe src="https://study-visuals-five.vercel.app/<course-folder>/<concept>.html" width="100%" height="820" style="border:0"></iframe>
   ```

   Adjust the height so the whole page fits without scrolling inside the frame.

## Content

- Language: English on the page (the owner's notes are in English). Explanations to the owner in chat can be in Chinese.
- Header: one-line title stating the idea; subtitle with course code + full course name, topic, and the example used.
- Example: small and concrete, preferably the lecture slides' own example. Say if values (e.g. memory addresses) are made up.
- Code panel: the real code, one line per `<div>`, including the call in `main` and the function header, so every parameter's value is visible.
- Steps: one step per meaningful change. Each step highlights the code line(s) running now and shows the state AFTER that line. Captions say what happens and why, in 1–3 sentences.
- Highlight the single thing that changes in a step (amber `--hot` / `--hotline`). Moving pointers (like `temp`) use `--temp`.
- Key points (bottom): 2–4 short rules worth remembering for the exam (why, order of operations, special cases).
- The code must be correct. If the lecture slides contain a bug, use the corrected version.
- Maths must be readable as maths, never raw text notation: write subscripts and superscripts with `<sub>` / `<sup>` in HTML (f<sub>x</sub>, e<sup>xy</sup>) and `<tspan baseline-shift="sub|super" font-size="...">` in SVG; use real symbols (−, ×, ÷, √, ≈, ⇒, Δ, ε₁). Not `f_x`, `e^(xy)`, `x^2`, `->`. For a panel of formulas instead of code, give the `<pre>` the `math` class (serif, wrapping) and set captions with `innerHTML`.

## Design and compatibility rules

- Keep the template's look (cobalt header, white panels, Space Grotesk + Inter + JetBrains Mono). Do not restyle a single page.
- Self-contained: CSS and JS inline, images as inline SVG. No other files, no build.
- Must work in a phone-width iframe (about 360 px) and in light and dark mode.
- Obsidian mobile uses an older browser engine. Therefore:
  - no `light-dark()`: use plain CSS variables plus `@media (prefers-color-scheme: dark)` (as in the template);
  - no `context-stroke` / `context-fill` in SVG markers: one `<marker>` per colour;
  - put `var(--x)` colours in SVG `style="fill:...;stroke:..."`, not in `fill=` / `stroke=` attributes;
  - one `style` attribute per element (a second one is ignored).
- Code font: keep `font-variant-ligatures:none` AFTER the `font:` shorthand, otherwise `->` and `!=` turn into arrows.
- In SVG, no text may overlap a line or another label.
- The site is public: never include personal information (names, student IDs, grades, schedules).

## Checklist before pushing

- [ ] The JS has no syntax errors (e.g. `node --check` on the script).
- [ ] Every step renders; Previous/Next/Restart and ← → keys work.
- [ ] Nothing overlaps; nothing overflows at 360 px width.
- [ ] Code shows `->` and `!=` literally.
- [ ] Page is listed in `index.html`.
- [ ] No `light-dark(` or `context-stroke` in the page's CSS/SVG.
