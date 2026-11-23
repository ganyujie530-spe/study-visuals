# study-visuals

Interactive, visual study notes. Live site: https://study-visuals-five.vercel.app Each note is one self-contained HTML page, deployed by Vercel and embedded in the Obsidian vault with an iframe.

## Structure

- `index.html` — list of all notes. Add every new page to the `courses` array.
- One folder per course, named by course code in lowercase (e.g. `cst108/` = CST108 Programming Practice).
- One page per concept, file name in kebab-case (e.g. `insert-at-end.html`).

## Rules for pages

- Self-contained: CSS and JS inline, no build step, no local images (use inline SVG).
- Text in English (same as the formal notes).
- Must work inside an iframe and on a phone; support light and dark mode.
- The site is public: never put personal information in it (name, student ID, grades, etc.).

## Embedding in Obsidian

Paste into a note (replace the path):

```html
<iframe src="https://study-visuals-five.vercel.app/cst108/insert-at-end.html" width="100%" height="760" style="border:0"></iframe>
```

## Deployment

Vercel project `study-visuals` is linked to this repo. Every push to `main` redeploys automatically. Vercel Authentication must stay off for production, or the iframe shows a login page.
