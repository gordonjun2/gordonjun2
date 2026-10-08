# GitHub Profile README — "Retro/byte-bit" Design

**Date:** 2026-10-09
**Status:** Approved (pending spec review)
**Goal:** Personal brand / fun. A GitHub profile front page with old-web, byte-bit personality that renders correctly in both light and dark themes.

## Overview

Create the public repo `gordonjun2/gordonjun2` whose `README.md` renders as Gordon's GitHub profile front page. The aesthetic is retro/byte-bit: pixel art, GIFs, 88x31 buttons, old-web chrome. All motion comes from GIF/SVG animation only — GitHub strips JavaScript and CSS. Every raster/SVG image is theme-adaptive via `<picture>` + `prefers-color-scheme`.

## Approach (approved: A — hybrid)

- Hosted services for stats and badges (`github-readme-stats`, `komarev`, `shields.io`), color-tuned per theme.
- Retro chrome (banners, buttons, pixel art) hand-crafted as SVG/PNG committed under `assets/`, self-hosted in-repo so hotlink rot is impossible and theme variants are exact.

## Repository layout

```
gordonjun2/                     # public GitHub repo
├── README.md                   # the profile page
├── LICENSE                     # MIT (content is public-facing)
└── assets/
    ├── light/                  # theme variants tuned for light mode
    └── dark/                   # same filenames, dark-tuned
```

File naming mirrors between `assets/light/` and `assets/dark/` so `<picture>` sources stay symmetrical.

## README content blocks (top to bottom)

### 1. Pixel whoami intro
- Theme-adaptive SVG banner: pixel-font title `GORDON_OH.EXE`, subtitle "has entered the chat", blinking-cursor animation (SVG `<animate>`).
- One-liner under the banner: `> whoami` → approved copy: builder of bots, wrangler of LLMs, degen by night (final wording confirmed with Gordon before shipping).

### 2. Now building
- Public repos as "cartridge" rows (name — one-liner — link):
  - `tg_sentinel` — Python Telegram automation/sentinel bot
  - `crypto-trading-analysis` — Jupyter-based market analysis notebooks
  - `tracectrl` — HTML web experiment
  - `agentic-builders-collective.github.io` — collective site (Astro)
- Private teasers, plain text with `[STEALTH]` tag, no links:
  - serendip-tg — AI matchmaking Telegram mini-app
  - AIED — adaptive AI learning platform
  - shorts-gen-wealth — short-form finance content pipeline
- One-liners above are drafts; Gordon confirms exact copy at review.

### 3. Tech stack badges
- `> loadout:` label + shields.io flat-square badges, retro color palette:
  Python, FastAPI, React, TypeScript, Celery, SQLAlchemy, pgvector, Docker, Supabase, Telegram Bot API.
- Same badge URLs for both themes (shields flat style is legible on both); no `<picture>` needed.

### 4. Retro stats
- Two `github-readme-stats` cards (top languages + streak stats) wrapped in `<picture>` with `&theme=` swapped per theme so card colors match the hand-drawn SVG chrome.
- Framed with a retro border SVG or ASCII frame in markdown.

### 5. Crypto corner
- Header: `trust_me_bro.csv` in code style.
- Pixel chart GIF (theme-agnostic: white/light background so it survives both themes).
- 88x31-style "NOT FINANCIAL ADVICE" disclaimer button (SVG, theme-adaptive).

### 6. Old-web footer
- Hand-drawn 88x31 SVG buttons: "BEST VIEWED IN 1996", "NOW WITH 100% MORE VIBES".
- Visitor counter via komarev (`visitor badge`), retro-styled.
- Under-construction GIF (theme-agnostic).
- No `<marquee>` (GitHub strips it); motion only via GIF/SVG.

### 7. Contact arcade
- `> INSERT COIN TO CONNECT:` line.
- "PRESS START" pixel link → `mailto:gordonoh@yahoo.com.sg`.

## Theme-adaptive mechanism (mandatory pattern)

Every theme-dependent image uses:

```markdown
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/dark/name.svg">
  <img src="assets/light/name.svg" alt="...">
</picture>
```

Theme-agnostic assets (GIFs with light backgrounds, shields badges) are used directly.

## Constraints

- No JavaScript, no CSS, no `<style>`, no `<marquee>` — stripped by GitHub.
- All assets referenced via relative paths (`assets/...`) so the repo renders correctly on github.com.
- No GitHub Actions / automation in v1 (YAGNI).
- Total asset weight target: < 1 MB.

## Error handling / failure modes

- Hotlinked services (shields, komarev, github-readme-stats) down → badge/card shows service error image; acceptable degradation, self-hosted chrome still renders.
- Light/dark mismatch → mitigated by the `<picture>` pattern; verify both themes during review (GitHub settings or browser devtools emulation).

## Testing / acceptance

1. Push to a scratch branch or view rendered locally (VS Code Markdown preview approximates; final check on github.com after publish).
2. Toggle light/dark → all images swap correctly, no white/black boxes.
3. All links resolve (repos, mailto).
4. README renders within GitHub sanitization rules (no stripped-tag artifacts).

## Out of scope (v1)

- Guestbook/issues interaction block (declined).
- GitHub Actions automation (snake animation, auto-updating stats).
- Custom domain / profile pictures / bio changes outside README.
