# SmartSchool — Landing Page

Marketing landing page for **SmartSchool**, a complete school management system built for
schools in Pakistan — QR-code attendance with instant WhatsApp updates to parents, fee
challans, results, salaries and reports.

## What this is

A single-file static website. No framework, no build step, no dependencies.

```
.
├── index.html    # the entire site — markup, CSS and JS inline
├── favicon.svg   # site icon
├── og-image.png  # 1200×630 social sharing preview
├── README.md
└── .gitignore
```

Everything lives in `index.html`: the styles are in one `<style>` block and the
animations/interactions are in one `<script>` block at the bottom. Fonts (Fraunces,
Public Sans, IBM Plex Mono) load from Google Fonts.

## Running it locally

Open the file directly:

```bash
open index.html
```

Or serve it, which more closely matches production (root-relative paths like
`/favicon.svg` resolve properly):

```bash
python3 -m http.server 8000
# → http://localhost:8000
```

## Deployment

Deployed on **Vercel** as a zero-config static site. Vercel serves `index.html` from the
repository root as-is — there is no build command and no output directory to configure,
so the project intentionally has no `vercel.json`, no `package.json` and no bundler.

Pushes to the default branch deploy automatically once the repo is connected to Vercel.

## Editing

Edit `index.html` directly. Because there is no build step, whatever is committed is
exactly what is served.

Two things to update after pointing a real domain at the site — both near the top of the
`<head>` in `index.html`:

- `<link rel="canonical">` and `og:url`
- `og:image` and `twitter:image` (these need absolute URLs to render in link previews)

Replace the `https://smartschool-website.vercel.app/` placeholder in each.
