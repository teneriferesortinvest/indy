# Proyecto Indy — landing page

A single-page site for the YouTube channel **@proyectoindy** — a reverse-chronological timeline of `reportajes` plus an Instagram strip, modelled after [pg-lang.com](https://pg-lang.com) with a warm cream-and-gold palette.

**Live:** https://teneriferesortinvest.github.io/indy/

## What this is

- `index.html` — the entire site (HTML + inline CSS + ~50 lines of vanilla JS).
- `assets/ig/` — 5 Instagram cover images served locally.
- No build step, no framework, no CMS, no analytics.
- Click any video headline or thumbnail → opens an inline YouTube modal (privacy-friendly `youtube-nocookie.com`). Esc / backdrop / close button to dismiss.

## File map

```
.
├── index.html         ← the entire site
├── assets/
│   └── ig/            ← Instagram cover images (5 jpg files)
└── README.md          ← this file
```

## How to update content

### Add or remove a video

Open `index.html`, find the `<main class="entries">` block, and copy one of the existing `<article class="entry">` blocks. Each entry needs four things:

1. `data-video-id` — the YouTube video ID (e.g. `KrPih7GUJQM` from `youtube.com/watch?v=KrPih7GUJQM`).
2. `data-video-title` — a short title for the modal accessibility label.
3. `href` — the public YouTube URL.
4. Thumbnail `src` — point to `https://i.ytimg.com/vi/{VIDEO_ID}/maxresdefault.jpg`.

Place new entries **at the top** of the timeline (newest first).

### Change the email on the Contacto line

Currently shipping with `[email pendiente de confirmación]` because the channel has no public address. Once an email is chosen:

1. Search `index.html` for `data-email-placeholder`.
2. Replace the placeholder line with:
   ```html
   <p><a href="mailto:NEW@EMAIL.com">NEW@EMAIL.com</a></p>
   ```

### Edit masthead or footer copy

Locked strings (do not paraphrase):

- Masthead opener: `Por fin empieza Indy. Por fin empiezan las aventuras.` (verbatim from the Marruecos cold open)
- Footer tagline: `Nos vemos antes de lo que ustedes creen.` (his recurring sign-off)

### Swap an Instagram tile

1. Replace the corresponding cover image in `assets/ig/cover-{shortcode}.jpg` (640×640 jpg, ~10 KB).
2. Update the `href`, `alt`, and `<span class="ig-date">` text on the matching `<a class="tile">` in `index.html`.

The Instagram grid is hand-built (5 entries). 3 columns desktop (3-2 wrap), 2 columns on most mobiles, 1 column below 380px.

## How to deploy

### GitHub Pages

This repo is already wired to GitHub Pages. Push to `main` and the site rebuilds within ~1 minute. To enable Pages from scratch on a fresh repo:

```bash
gh api repos/<owner>/<repo>/pages -X POST -f source[branch]=main -f source[path]=/
```

### Anywhere else

Static single-page site. Drop `index.html` and `assets/` into any static host (Netlify, Cloudflare Pages, Vercel, plain S3+CloudFront, a VPS with nginx). No environment variables, no build command.

### Local preview

```bash
python3 -m http.server 8000
# visit http://localhost:8000/
```

You can also open `index.html` directly in a browser via `file://`, but the YouTube iframe will be blocked by some browsers' file-origin policy — use the local server.

## Design notes

- Palette: cream `#f6ecc9` background, dark brown `#1a1407` text, dark gold `#b8860b` links.
- Type: `ui-monospace, SFMono-Regular, "SF Mono", Menlo, Consolas, monospace` throughout.
- Max content width 720px; no images expand wider than the column.
- Mobile breakpoint at 640px (padding + gap shrink); Instagram grid drops to 2 cols, then 1.
- Modal uses `youtube-nocookie.com` to avoid setting tracking cookies until the viewer actually plays.

## What's intentionally NOT here

- No About / bio section.
- No newsletter signup, no lead capture, no analytics.
- No multi-language toggle (page is Spanish only).
- No CMS — content lives in HTML.

## Credits

Channel + Instagram content: **@proyectoindy** (Indy).
Inspiration: [pg-lang.com](https://pg-lang.com).
