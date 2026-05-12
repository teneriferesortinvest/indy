# Proyecto Indy — landing page

A single-page site for the YouTube channel **@proyectoindy** — a reverse-chronological timeline of `reportajes` plus an Instagram link, modelled after [pg-lang.com](https://pg-lang.com) with a warm cream-and-gold palette.

**Live:** https://teneriferesortinvest.github.io/indy/

## What this is

- `index.html` — the entire site (HTML + inline CSS + ~80 lines of vanilla JS).
- No build step, no framework, no CMS, no analytics.
- Click any video headline → opens an inline YouTube modal (privacy-friendly `youtube-nocookie.com`). Esc / backdrop / close button to dismiss.
- The timeline is **text-only**: date + clickable headline per entry. No thumbnails. This is intentional — it keeps the page fast, lets the headlines breathe, and ducks YouTube's broken vertical-Shorts thumbnail problem.

## File map

```
.
├── index.html   ← the entire site
└── README.md    ← this file
```

## How to update content

### Add or remove a video

Open `index.html`, find the `<main class="entries">` block, and copy one of the existing `<article class="entry">` blocks. Each entry needs:

1. A date line: `<p class="date">14 nov 2025 · Egipto</p>` — Spanish format `<day> <mon> <year>`, then optional `· <location>`, plus `· short` if it's a YouTube Short.
2. A title with `data-video-id` (the YouTube ID), `data-video-title` (used for the modal label), and a real `href` to the public YouTube URL.

Place new entries **at the top** of the timeline (newest first). Spanish month abbreviations: `ene feb mar abr may jun jul ago sep oct nov dic`.

### Change the email on the Contacto line

Edit the `mailto:` link in the `<section class="contact">` block of `index.html`.

### Edit masthead or footer copy

Locked strings (do not paraphrase):

- Masthead opener: `Por fin empieza Indy. Por fin empiezan las aventuras.` (verbatim from the Marruecos cold open)
- Footer tagline: `Nos vemos antes de lo que ustedes creen.` (his recurring sign-off)

### Update the Instagram link

The Instagram section is a single line: `<a href="https://instagram.com/proyectoindy" target="_blank">@proyectoindy →</a>`. Change the handle/URL in two places (the IG section and the footer `Instagram` link) if Indy ever moves.

## How to deploy

### GitHub Pages

This repo is already wired to GitHub Pages. Push to `main` and the site rebuilds within ~1 minute. To enable Pages from scratch on a fresh repo:

```bash
gh api repos/<owner>/<repo>/pages -X POST -f source[branch]=main -f source[path]=/
```

### Anywhere else

Static single-page site. Drop `index.html` into any static host (Netlify, Cloudflare Pages, Vercel, plain S3+CloudFront, a VPS with nginx). No environment variables, no build command.

### Local preview

```bash
python3 -m http.server 8000
# visit http://localhost:8000/
```

You can also open `index.html` directly via `file://`, but the YouTube iframe will be blocked by some browsers' file-origin policy — use the local server.

## Design notes

- Palette: cream `#f6ecc9` background, dark brown `#1a1407` text, deep brown `#5c4400` links (WCAG AA 7.4:1 contrast).
- Type: `ui-monospace, SFMono-Regular, "SF Mono", Menlo, Consolas, monospace` throughout.
- Max content width 720px.
- Mobile breakpoint at 640px (padding + gap shrink).
- Modal: `youtube-nocookie.com` embed; Tab/Shift+Tab cycle inside the dialog (focus trap); Esc / backdrop / × dismiss; iframe `src` reset to `about:blank` on close so audio stops. 8-second load-timeout falls back to a "Ver en YouTube" link if the embed fails to load.
- Cmd/Ctrl/Shift/Alt/middle-click on a headline → opens YouTube in a new tab (native browser affordance, not intercepted).

## What's intentionally NOT here

- No About / bio section.
- No video thumbnails on the timeline (text-only by design).
- No newsletter signup, no lead capture, no analytics.
- No multi-language toggle (page is Spanish only).
- No CMS — content lives in HTML.

## Credits

Channel + Instagram content: **@proyectoindy** (Indy).
Inspiration: [pg-lang.com](https://pg-lang.com).
