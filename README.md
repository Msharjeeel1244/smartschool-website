# SmartSchool — Landing Page

Marketing landing page for **SmartSchool**, a complete school management system built for
schools in Pakistan — QR-code attendance with instant WhatsApp updates to parents, fee
challans, results, salaries and reports.

## What this is

A single-file static website. No framework, no build step, no dependencies.

```
.
├── index.html    # the entire site (self-extracting bundle, ~3 MB)
├── favicon.svg   # site icon
├── og-image.png  # 1200×630 social sharing preview
├── README.md
└── .gitignore
```

`index.html` is an exported **bundle**: a small loader plus the page's real markup, CSS
and assets packed into `<script type="__bundler/…">` blocks. On load, the loader unpacks
those and swaps the document for the finished page. It is still one self-contained static
file — nothing is fetched from a server and there is nothing to build — but it does
require JavaScript to render.

Because the body is assembled at runtime, the SEO and social tags are written **twice**:
once inside the bundle, and once as plain tags in the static `<head>` at the top of the
file. The static copies are the ones that matter — crawlers (WhatsApp, Facebook, Twitter,
LinkedIn) do not run JavaScript and would otherwise see an empty page. Keep them in sync
with the bundled ones.

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

To change the page content, edit the original source the bundle was exported from and
re-export, then replace `index.html` — hand-editing the packed `__bundler` blocks is not
practical. After replacing it, re-add the static `<head>` tags described above, since a
fresh export only carries the bundled copies.

Two things to update after pointing a real domain at the site — both in the static
`<head>` at the top of `index.html`:

- `<link rel="canonical">` and `og:url`
- `og:image` and `twitter:image` (these need absolute URLs to render in link previews)

Replace the `https://smartschool-website.vercel.app/` placeholder in each.
