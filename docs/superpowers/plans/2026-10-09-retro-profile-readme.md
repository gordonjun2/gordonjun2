# Retro Profile README Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build the `gordonjun2/gordonjun2` public repo whose README renders a retro/byte-bit GitHub profile front page, theme-adaptive for light and dark mode.

**Architecture:** Single README.md referencing hand-crafted SVG assets committed under `assets/` (light/dark variants for theme-dependent art, root-level for theme-agnostic art). Hosted services only for stats/badges/counter. No JS/CSS/marquee — GitHub strips them; all motion via SVG SMIL animation.

**Tech Stack:** Markdown, SVG (SMIL), shields.io, github-readme-stats, komarev, gh CLI.

**Working directory for every task:** `/Users/gordonjun/Desktop/Projects/gordonjun2`

**Spec:** `docs/superpowers/specs/2026-10-09-github-profile-readme-design.md`

---

### Task 1: LICENSE

**Files:**
- Create: `LICENSE`

- [ ] **Step 1: Write LICENSE (MIT, full text)**

```
MIT License

Copyright (c) 2026 Gordon Oh

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

- [ ] **Step 2: Commit**

```bash
git add LICENSE && git commit -m "chore: add MIT license"
```

Expected: commit succeeds.

---

### Task 2: Theme banner (light + dark)

**Files:**
- Create: `assets/light/banner.svg`
- Create: `assets/dark/banner.svg`

- [ ] **Step 1: Create directories**

```bash
mkdir -p assets/light assets/dark
```

- [ ] **Step 2: Write `assets/light/banner.svg`**

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="700" height="170" viewBox="0 0 700 170" role="img" aria-label="GORDON_OH.EXE has entered the chat">
  <defs>
    <pattern id="grid" width="14" height="14" patternUnits="userSpaceOnUse">
      <rect width="2" height="2" fill="#24292f" opacity="0.18"/>
    </pattern>
  </defs>
  <rect width="700" height="170" fill="url(#grid)"/>
  <g transform="translate(34,45)" shape-rendering="crispEdges">
    <rect x="0" y="0" width="80" height="20" fill="#24292f"/>
    <rect x="0" y="20" width="80" height="60" fill="#f1c27d"/>
    <rect x="0" y="0" width="10" height="80" fill="#24292f"/>
    <rect x="70" y="0" width="10" height="80" fill="#24292f"/>
    <rect x="0" y="70" width="80" height="10" fill="#24292f"/>
    <rect x="10" y="35" width="20" height="10" fill="#24292f"/>
    <rect x="50" y="35" width="20" height="10" fill="#24292f"/>
    <rect x="25" y="55" width="30" height="10" fill="#24292f"/>
  </g>
  <text x="140" y="86" font-family="'Courier New',Courier,monospace" font-weight="bold" font-size="42" letter-spacing="2" fill="#24292f">GORDON_OH.EXE</text>
  <rect x="504" y="52" width="20" height="38" fill="#e94560">
    <animate attributeName="opacity" values="1;1;0;0" keyTimes="0;0.5;0.5;1" dur="1.1s" repeatCount="indefinite"/>
  </rect>
  <text x="142" y="122" font-family="'Courier New',Courier,monospace" font-size="17" fill="#57606a">&gt; has entered the chat_</text>
</svg>
```

- [ ] **Step 3: Write `assets/dark/banner.svg`** (same geometry; dark-tuned colors)

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="700" height="170" viewBox="0 0 700 170" role="img" aria-label="GORDON_OH.EXE has entered the chat">
  <defs>
    <pattern id="grid" width="14" height="14" patternUnits="userSpaceOnUse">
      <rect width="2" height="2" fill="#e6edf3" opacity="0.12"/>
    </pattern>
  </defs>
  <rect width="700" height="170" fill="url(#grid)"/>
  <g transform="translate(34,45)" shape-rendering="crispEdges">
    <rect x="0" y="0" width="80" height="20" fill="#8b949e"/>
    <rect x="0" y="20" width="80" height="60" fill="#f1c27d"/>
    <rect x="0" y="0" width="10" height="80" fill="#8b949e"/>
    <rect x="70" y="0" width="10" height="80" fill="#8b949e"/>
    <rect x="0" y="70" width="80" height="10" fill="#8b949e"/>
    <rect x="10" y="35" width="20" height="10" fill="#24292f"/>
    <rect x="50" y="35" width="20" height="10" fill="#24292f"/>
    <rect x="25" y="55" width="30" height="10" fill="#24292f"/>
  </g>
  <text x="140" y="86" font-family="'Courier New',Courier,monospace" font-weight="bold" font-size="42" letter-spacing="2" fill="#e6edf3">GORDON_OH.EXE</text>
  <rect x="504" y="52" width="20" height="38" fill="#7ee787">
    <animate attributeName="opacity" values="1;1;0;0" keyTimes="0;0.5;0.5;1" dur="1.1s" repeatCount="indefinite"/>
  </rect>
  <text x="142" y="122" font-family="'Courier New',Courier,monospace" font-size="17" fill="#8b949e">&gt; has entered the chat_</text>
</svg>
```

- [ ] **Step 4: Verify both files are valid XML and small**

```bash
python3 -c "import xml.etree.ElementTree as ET; ET.parse('assets/light/banner.svg'); ET.parse('assets/dark/banner.svg'); print('XML OK')" && du -sh assets/
```

Expected output: `XML OK` and total well under 1 MB (banner pair ≈ 3 KB).

- [ ] **Step 5: Commit**

```bash
git add assets/light/banner.svg assets/dark/banner.svg && git commit -m "feat: pixel whoami banner (light/dark)"
```

---

### Task 3: 88x31 buttons

**Files:**
- Create: `assets/btn-1996.svg`
- Create: `assets/btn-vibes.svg`
- Create: `assets/btn-nfa.svg`

All three are theme-agnostic (solid black face, white text) — used directly, no `<picture>`.

- [ ] **Step 1: Write `assets/btn-1996.svg`**

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="88" height="31" viewBox="0 0 88 31" role="img" aria-label="Best viewed in 1996">
  <rect x="0.5" y="0.5" width="87" height="30" fill="#000000" stroke="#ffffff"/>
  <rect x="2.5" y="2.5" width="83" height="26" fill="none" stroke="#3ea6ff"/>
  <text x="44" y="13" text-anchor="middle" font-family="'Courier New',Courier,monospace" font-weight="bold" font-size="8" fill="#ffffff">BEST VIEWED IN</text>
  <text x="44" y="25" text-anchor="middle" font-family="'Courier New',Courier,monospace" font-weight="bold" font-size="10" fill="#3ea6ff">1996</text>
</svg>
```

- [ ] **Step 2: Write `assets/btn-vibes.svg`**

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="88" height="31" viewBox="0 0 88 31" role="img" aria-label="Now with 100 percent more vibes">
  <rect x="0.5" y="0.5" width="87" height="30" fill="#000000" stroke="#ffffff"/>
  <rect x="2.5" y="2.5" width="83" height="26" fill="none" stroke="#ffd23f"/>
  <text x="44" y="13" text-anchor="middle" font-family="'Courier New',Courier,monospace" font-weight="bold" font-size="8" fill="#ffffff">NOW WITH 100%</text>
  <text x="44" y="25" text-anchor="middle" font-family="'Courier New',Courier,monospace" font-weight="bold" font-size="10" fill="#ffd23f">MORE VIBES</text>
</svg>
```

- [ ] **Step 3: Write `assets/btn-nfa.svg`**

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="88" height="31" viewBox="0 0 88 31" role="img" aria-label="Not financial advice">
  <rect x="0.5" y="0.5" width="87" height="30" fill="#000000" stroke="#ffffff"/>
  <rect x="2.5" y="2.5" width="83" height="26" fill="none" stroke="#ff5252"/>
  <g shape-rendering="crispEdges">
    <rect x="6" y="18" width="4" height="6" fill="#2ea043"/>
    <rect x="11" y="14" width="4" height="10" fill="#2ea043"/>
    <rect x="16" y="10" width="4" height="14" fill="#2ea043"/>
  </g>
  <text x="53" y="14" text-anchor="middle" font-family="'Courier New',Courier,monospace" font-weight="bold" font-size="8" fill="#ffffff">NOT FINANCIAL</text>
  <text x="53" y="24" text-anchor="middle" font-family="'Courier New',Courier,monospace" font-weight="bold" font-size="9" fill="#ff5252">ADVICE</text>
</svg>
```

- [ ] **Step 4: Verify XML validity**

```bash
python3 -c "import xml.etree.ElementTree as ET; [ET.parse(f) for f in ['assets/btn-1996.svg','assets/btn-vibes.svg','assets/btn-nfa.svg']]; print('XML OK')"
```

Expected output: `XML OK`

- [ ] **Step 5: Commit**

```bash
git add assets/btn-*.svg && git commit -m "feat: 88x31 retro buttons"
```

---

### Task 4: Animated theme-agnostic art (chart + construction)

**Files:**
- Create: `assets/chart.svg`
- Create: `assets/under-construction.svg`

- [ ] **Step 1: Write `assets/chart.svg`** (white terminal panel survives both themes; candles ascend, text blinks)

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="560" height="230" viewBox="0 0 560 230" role="img" aria-label="Pixel chart going up">
  <rect x="0.5" y="0.5" width="559" height="229" rx="4" fill="#ffffff" stroke="#24292f"/>
  <rect x="1" y="1" width="558" height="24" rx="4" fill="#e2e5e9"/>
  <circle cx="14" cy="13" r="4" fill="#e5534b"/>
  <circle cx="28" cy="13" r="4" fill="#ffd23f"/>
  <circle cx="42" cy="13" r="4" fill="#2ea043"/>
  <text x="60" y="17" font-family="'Courier New',Courier,monospace" font-size="11" fill="#24292f">trust_me_bro.csv</text>
  <g shape-rendering="crispEdges">
    <rect x="36" y="140" width="2" height="40" fill="#24292f"/>
    <rect x="30" y="150" width="14" height="20" fill="#2ea043"/>
    <rect x="86" y="115" width="2" height="45" fill="#24292f"/>
    <rect x="80" y="125" width="14" height="25" fill="#2ea043"/>
    <rect x="136" y="125" width="2" height="40" fill="#24292f"/>
    <rect x="130" y="135" width="14" height="20" fill="#e5534b"/>
    <rect x="186" y="90" width="2" height="50" fill="#24292f"/>
    <rect x="180" y="100" width="14" height="30" fill="#2ea043"/>
    <rect x="236" y="60" width="2" height="55" fill="#24292f"/>
    <rect x="230" y="70" width="14" height="35" fill="#2ea043"/>
    <rect x="286" y="42" width="2" height="48" fill="#24292f"/>
    <rect x="280" y="50" width="14" height="30" fill="#2ea043"/>
  </g>
  <g shape-rendering="crispEdges">
    <rect x="464" y="54" width="24" height="8" fill="#ffd23f"/>
    <rect x="456" y="62" width="40" height="8" fill="#ffd23f"/>
    <rect x="448" y="70" width="56" height="8" fill="#ffd23f"/>
    <rect x="456" y="78" width="40" height="8" fill="#ffd23f"/>
    <rect x="464" y="86" width="24" height="8" fill="#ffd23f"/>
    <rect x="472" y="62" width="24" height="24" fill="#ffffff"/>
  </g>
  <text x="440" y="205" font-family="'Courier New',Courier,monospace" font-weight="bold" font-size="13" fill="#e5534b">TO THE MOON
    <animate attributeName="opacity" values="1;0.25;1" dur="1.4s" repeatCount="indefinite"/>
  </text>
  <text x="30" y="205" font-family="'Courier New',Courier,monospace" font-size="11" fill="#57606a">+9999.42%</text>
</svg>
```

- [ ] **Step 2: Write `assets/under-construction.svg`**

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="360" height="36" viewBox="0 0 360 36" role="img" aria-label="Under construction">
  <defs>
    <pattern id="stripes" width="16" height="16" patternUnits="userSpaceOnUse" patternTransform="rotate(45)">
      <rect width="16" height="16" fill="#ffd23f"/>
      <rect width="8" height="16" fill="#24292f"/>
    </pattern>
  </defs>
  <rect x="1" y="1" width="358" height="34" fill="url(#stripes)" stroke="#24292f"/>
  <rect x="88" y="6" width="184" height="24" fill="#24292f"/>
  <text x="180" y="22" text-anchor="middle" font-family="'Courier New',Courier,monospace" font-weight="bold" font-size="11" fill="#ffd23f">UNDER CONSTRUCTION
    <animate attributeName="opacity" values="1;0.35;1" dur="1.2s" repeatCount="indefinite"/>
  </text>
</svg>
```

- [ ] **Step 3: Verify XML validity**

```bash
python3 -c "import xml.etree.ElementTree as ET; [ET.parse(f) for f in ['assets/chart.svg','assets/under-construction.svg']]; print('XML OK')"
```

Expected output: `XML OK`

- [ ] **Step 4: Commit**

```bash
git add assets/chart.svg assets/under-construction.svg && git commit -m "feat: animated pixel chart + under construction banner"
```

---

### Task 5: README.md

**Files:**
- Create: `README.md`

- [ ] **Step 1: Write `README.md` with the complete content below**

```markdown
<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/dark/banner.svg">
  <img alt="GORDON_OH.EXE — has entered the chat" src="assets/light/banner.svg" width="700">
</picture>

### `> whoami`

builder of bots · wrangler of LLMs · degen by night

---

### 🕹️ NOW BUILDING

| 🎮 CARTRIDGE | INFO |
| --- | --- |
| 📡 [tg_sentinel](https://github.com/gordonjun2/tg_sentinel) | Telegram sentinel bot (Python) |
| 📈 [crypto-trading-analysis](https://github.com/gordonjun2/crypto-trading-analysis) | market analysis in Jupyter |
| 🧪 [tracectrl](https://github.com/gordonjun2/tracectrl) | web experiment (HTML) |
| 🌐 [agentic-builders-collective.github.io](https://github.com/gordonjun2/agentic-builders-collective.github.io) | builders collective site (Astro) |
| 🔒 serendip-tg `[STEALTH]` | AI matchmaking Telegram mini-app — ask me about it |
| 🔒 aied `[STEALTH]` | adaptive AI learning platform |
| 🔒 shorts-gen-wealth `[STEALTH]` | short-form finance content pipeline |

### 🧰 LOADOUT

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-05948C?style=flat-square&logo=fastapi&logoColor=white)
![React](https://img.shields.io/badge/React-3B3B3B?style=flat-square&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-1E2A4A?style=flat-square&logo=typescript&logoColor=white)
![Celery](https://img.shields.io/badge/Celery-37814A?style=flat-square&logo=celery&logoColor=white)
![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-8B0000?style=flat-square&logo=sqlalchemy&logoColor=white)
![pgvector](https://img.shields.io/badge/pgvector-336791?style=flat-square&logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-1D63ED?style=flat-square&logo=docker&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?style=flat-square&logo=supabase&logoColor=white)
![Telegram](https://img.shields.io/badge/Telegram_Bot_API-2AABEE?style=flat-square&logo=telegram&logoColor=white)

<table>
  <tr>
    <td width="50%">
      <picture>
        <source media="(prefers-color-scheme: dark)" srcset="https://github-readme-stats.vercel.app/api?username=gordonjun2&show_icons=true&hide_border=true&count_private=true&theme=github_dark">
        <img alt="GitHub stats" src="https://github-readme-stats.vercel.app/api?username=gordonjun2&show_icons=true&hide_border=true&count_private=true&theme=default">
      </picture>
    </td>
    <td width="50%">
      <picture>
        <source media="(prefers-color-scheme: dark)" srcset="https://github-readme-stats.vercel.app/api/top-langs/?username=gordonjun2&layout=compact&hide_border=true&theme=github_dark">
        <img alt="Top languages" src="https://github-readme-stats.vercel.app/api/top-langs/?username=gordonjun2&layout=compact&hide_border=true&theme=default">
      </picture>
    </td>
  </tr>
</table>

### 📈 CRYPTO CORNER

`$ cat trust_me_bro.csv`

<img alt="pixel chart going up" src="assets/chart.svg" width="560">

<img alt="not financial advice" src="assets/btn-nfa.svg" width="88">

### 🚧 OLD WEB ZONE

<img alt="best viewed in 1996" src="assets/btn-1996.svg" width="88">
<img alt="now with 100 percent more vibes" src="assets/btn-vibes.svg" width="88">

<img alt="under construction" src="assets/under-construction.svg" width="360">

![profile views](https://komarev.com/ghpvc/?username=gordonjun2&style=for-the-badge&color=blueviolet)

### 👾 CONTACT

`> INSERT COIN TO CONNECT:` [▶ PRESS START](mailto:gordonoh@yahoo.com.sg)

</div>
```

- [ ] **Step 2: Verify every local asset path referenced exists**

```bash
grep -o 'assets/[a-zA-Z0-9_./-]*' README.md | sort -u | while read f; do test -f "$f" && echo "OK   $f" || echo "MISS $f"; done
```

Expected: every line starts with `OK` — exactly 7 files: `assets/btn-1996.svg`, `assets/btn-nfa.svg`, `assets/btn-vibes.svg`, `assets/chart.svg`, `assets/dark/banner.svg`, `assets/light/banner.svg`, `assets/under-construction.svg`.

- [ ] **Step 3: Verify no GitHub-stripped tags or scripts**

```bash
grep -Ein "<style|<script|<marquee|javascript:" README.md; echo "exit=$?"
```

Expected: no matches, `exit=1`.

- [ ] **Step 4: Verify all remote links are well-formed**

```bash
grep -o 'https://[^)"]*' README.md | sort -u
```

Expected: 17 URLs across github.com repos (4), shields.io (10), github-readme-stats (4: 2 light + 2 dark across two cards — note top-langs appears twice), komarev (1); all start with `https://`.

- [ ] **Step 5: Commit**

```bash
git add README.md && git commit -m "feat: retro byte-bit profile README"
```

---

### Task 6: Publish and verify

**Files:** none created (publish only)

- [ ] **Step 1: Create the public GitHub repo and push**

```bash
gh repo create gordonjun2/gordonjun2 --public --source=. --push --description "retro byte-bit profile // has entered the chat"
```

Expected: output contains `https://github.com/gordonjun2/gordonjun2` and push succeeds (`main` branch).

- [ ] **Step 2: Acceptance check (manual, in browser)**

1. Open https://github.com/gordonjun2 — README renders on the profile.
2. Toggle theme (Settings → Appearance, or browser devtools `prefers-color-scheme` emulation): banner text/cursor swap, both stats cards swap themes, no white/black boxes anywhere.
3. All 4 public repo links resolve; `mailto:` link opens composer.
4. Blinking cursor, "TO THE MOON" and "UNDER CONSTRUCTION" animations play.
5. No broken-image icons (all assets served from the repo itself).

---

## Self-Review

- **Spec coverage:** banner/whoami (T2, T5), now-building public+stealth rows (T5), loadout badges (T5), themed stats (T5), crypto corner incl. NFA button (T3, T4, T5), old-web footer incl. buttons + counter + construction (T3, T4, T5), contact arcade (T5), theme-adaptive `<picture>` pattern (T2, T5), no-JS/CSS constraint (T5 verification), < 1 MB assets (T2 check), publish + acceptance (T6). Guestbook and Actions correctly absent (out of scope per spec).
- **Placeholder scan:** none — all file contents are complete in the plan; "one-liners confirmed with Gordon" from the spec is resolved by the fixed copy in T5, which Gordon reviews at spec/plan approval.
- **Type consistency:** asset filenames used in README (T5) match files created in T2–T4 exactly (`banner.svg` light/dark, `btn-1996.svg`, `btn-vibes.svg`, `btn-nfa.svg`, `chart.svg`, `under-construction.svg`).
