# study-visuals

Interactive, visual study notes. Live site: https://study-visuals-five.vercel.app

Each note is one self-contained HTML page, deployed by Vercel and embedded in the Obsidian vault with an iframe.

- **AI assistants: read [AI_GUIDE.md](AI_GUIDE.md) before adding or editing pages.** Start new pages from [`_template/stepper.html`](_template/stepper.html).
- `index.html` lists all pages by course.
- One folder per course, named by course code in lowercase (e.g. `cst108/` = CST108 Programming Practice).

## Embedding in Obsidian

Paste into a note (replace the path), then move the cursor off the line:

```html
<iframe src="https://study-visuals-five.vercel.app/cst108/insert-at-end.html" width="100%" height="760" style="border:0"></iframe>
```

## Deployment

Vercel project `study-visuals` is linked to this repo. Every push to `main` redeploys automatically. Vercel Authentication must stay off for production, or the iframe shows a login page.
