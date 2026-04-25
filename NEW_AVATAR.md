# Adding a New J.A.R.V.I.S. Persona

Each persona is a self-contained product page (`{name}.html`) backed by its own JSON data file (`{name}-data.json`). The hub (`index.html`) shows a full-bleed comic-book cover card for every persona; hovering reveals the raw cover art and a CTA button.

---

## Step 1 — Get a Comic Cover Image

Find a **portrait-oriented** comic book cover or character art for your hero. Requirements:

| Requirement | Detail |
|---|---|
| Format | JPEG or **WebP** (both work in all modern browsers) |
| Minimum size | 800 × 1200 px (portrait) |
| Ideal size | 1500 × 2200 px or larger |
| Style | Comic cover art — not a movie still or close-up face shot |

**Finding images (no API key needed):**
- **Marvel characters** — `cdn.marvel.com/u/prod/marvel/i/mg/{hash}/clean.jpg` — full comic covers at 1821 × 2800 px
- **DC characters** — scrape `https://www.dc.com/characters/{slug}` for `static.dc.com` image URLs; filter for portrait `Char_Thumb_` or `Gallery` images and append `?w=1400`
- **Fandom CDN** — `https://static.wikia.nocookie.net/{wiki}/images/{path}/revision/latest/scale-to-width-down/800?cb={cb}` — returns WebP; rename `.webp`

Save the image to `docs/img/{character}.jpg` (or `.webp`).

---

## Step 2 — Create a Newspaper Hero SVG

Every product page has a newspaper-style banner behind the page header. Create `docs/img/newspaper-{name}.svg`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1200 400" preserveAspectRatio="xMidYMid slice">
  <rect width="1200" height="400" fill="#f0e6c8"/>
  <!-- top border -->
  <rect x="18" y="13" width="1164" height="2.5" fill="#111"/>

  <!-- MASTHEAD — change to your newspaper name -->
  <text x="600" y="48" text-anchor="middle"
    font-family="Georgia,'Times New Roman',serif"
    font-size="34" font-weight="bold" letter-spacing="8" fill="#0a0a0a">THE [NEWSPAPER NAME]</text>
  <text x="22" y="48" font-family="Georgia,serif" font-size="10" fill="#444">VOL. I  ·  NO. 1</text>
  <text x="1178" y="48" text-anchor="end" font-family="Georgia,serif" font-size="10" fill="#444">[DATE]  ·  $2.50</text>

  <!-- masthead rules -->
  <rect x="18" y="56" width="1164" height="3.5" fill="#0a0a0a"/>
  <rect x="18" y="61" width="1164" height="0.9" fill="#0a0a0a"/>

  <!-- MAIN HEADLINE — hero does something impressive -->
  <text x="600" y="100" text-anchor="middle"
    font-family="Georgia,serif" font-size="34" font-weight="bold" fill="#080808">
    [HERO] SAVES THE DAY; [NAME] MODULE GOES LIVE
  </text>

  <!-- deck (italic sub-headline) -->
  <text x="600" y="120" text-anchor="middle"
    font-family="Georgia,serif" font-size="13.5" font-style="italic" fill="#2a2a2a">
    [Supporting detail 1] · [Supporting detail 2] · [Supporting detail 3]
  </text>

  <!-- section rule + column dividers -->
  <rect x="18" y="130" width="1164" height="0.7" fill="#666"/>
  <rect x="415" y="136" width="0.7" height="188" fill="#aaa"/>
  <rect x="790" y="136" width="0.7" height="188" fill="#aaa"/>

  <!-- COL 1 headline + body bars -->
  <text x="24" y="155" font-family="Georgia,serif" font-size="13.5" font-weight="bold" fill="#0a0a0a">[COL 1 HEADLINE LINE 1]</text>
  <text x="24" y="172" font-family="Georgia,serif" font-size="13.5" font-weight="bold" fill="#0a0a0a">[COL 1 HEADLINE LINE 2]</text>
  <rect x="24" y="180" width="374" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="24" y="190" width="374" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="24" y="200" width="338" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="24" y="210" width="374" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="24" y="220" width="296" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="24" y="230" width="374" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="24" y="240" width="355" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="24" y="250" width="374" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="24" y="260" width="280" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="24" y="270" width="374" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="24" y="280" width="340" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="24" y="290" width="374" height="5.5" rx="1.5" fill="#b8a882"/>

  <!-- COL 2 headline + body bars -->
  <text x="425" y="155" font-family="Georgia,serif" font-size="13.5" font-weight="bold" fill="#0a0a0a">[COL 2 HEADLINE LINE 1]</text>
  <text x="425" y="172" font-family="Georgia,serif" font-size="13.5" font-weight="bold" fill="#0a0a0a">[COL 2 HEADLINE LINE 2]</text>
  <rect x="425" y="180" width="348" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="425" y="190" width="348" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="425" y="200" width="310" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="425" y="210" width="348" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="425" y="220" width="276" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="425" y="230" width="348" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="425" y="240" width="330" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="425" y="250" width="348" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="425" y="260" width="265" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="425" y="270" width="348" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="425" y="280" width="318" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="425" y="290" width="348" height="5.5" rx="1.5" fill="#b8a882"/>

  <!-- COL 3 headline + body bars -->
  <text x="800" y="155" font-family="Georgia,serif" font-size="13.5" font-weight="bold" fill="#0a0a0a">[COL 3 HEADLINE LINE 1]</text>
  <text x="800" y="172" font-family="Georgia,serif" font-size="13.5" font-weight="bold" fill="#0a0a0a">[COL 3 HEADLINE LINE 2]</text>
  <rect x="800" y="180" width="378" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="800" y="190" width="378" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="800" y="200" width="340" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="800" y="210" width="378" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="800" y="220" width="305" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="800" y="230" width="378" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="800" y="240" width="358" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="800" y="250" width="378" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="800" y="260" width="275" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="800" y="270" width="378" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="800" y="280" width="345" height="5.5" rx="1.5" fill="#b8a882"/>
  <rect x="800" y="290" width="378" height="5.5" rx="1.5" fill="#b8a882"/>

  <!-- lower section rule -->
  <rect x="18" y="313" width="1164" height="0.7" fill="#666"/>

  <!-- lower headlines (3 across with column rules) -->
  <text x="24" y="331" font-family="Georgia,serif" font-size="11.5" font-weight="bold" fill="#111">[LOWER HEADLINE 1 LINE 1]</text>
  <text x="24" y="346" font-family="Georgia,serif" font-size="11.5" font-weight="bold" fill="#111">[LOWER HEADLINE 1 LINE 2]</text>
  <rect x="24" y="352" width="366" height="4" rx="1" fill="#c8b890"/>
  <rect x="24" y="359" width="366" height="4" rx="1" fill="#c8b890"/>
  <rect x="24" y="366" width="290" height="4" rx="1" fill="#c8b890"/>

  <rect x="408" y="316" width="0.7" height="64" fill="#bbb"/>
  <text x="418" y="331" font-family="Georgia,serif" font-size="11.5" font-weight="bold" fill="#111">[LOWER HEADLINE 2 LINE 1]</text>
  <text x="418" y="346" font-family="Georgia,serif" font-size="11.5" font-weight="bold" fill="#111">[LOWER HEADLINE 2 LINE 2]</text>
  <rect x="418" y="352" width="358" height="4" rx="1" fill="#c8b890"/>
  <rect x="418" y="359" width="358" height="4" rx="1" fill="#c8b890"/>
  <rect x="418" y="366" width="280" height="4" rx="1" fill="#c8b890"/>

  <rect x="793" y="316" width="0.7" height="64" fill="#bbb"/>
  <text x="803" y="331" font-family="Georgia,serif" font-size="11.5" font-weight="bold" fill="#111">[LOWER HEADLINE 3 LINE 1]</text>
  <text x="803" y="346" font-family="Georgia,serif" font-size="11.5" font-weight="bold" fill="#111">[LOWER HEADLINE 3 LINE 2]</text>
  <rect x="803" y="352" width="375" height="4" rx="1" fill="#c8b890"/>
  <rect x="803" y="359" width="375" height="4" rx="1" fill="#c8b890"/>
  <rect x="803" y="366" width="295" height="4" rx="1" fill="#c8b890"/>

  <!-- bottom rules -->
  <rect x="18" y="384" width="1164" height="2" fill="#111"/>
  <rect x="18" y="388" width="1164" height="0.7" fill="#555"/>
</svg>
```

The gradient overlay (Step 4) sits at ~75–80% opacity on top, so the ink-on-parchment newspaper bleeds through the theme colour.

---

## Step 3 — Define Your CSS Theme

Add this `:root` block inside the `<style>` tag of your `{name}.html`:

```css
:root {
  --bg:         [PAGE_BG];           /* e.g. #eef4ff */
  --surface:    #ffffff;
  --border:     rgba(R,G,B,.13);
  --muted:      [SECONDARY_TEXT];    /* e.g. #4a6285 */
  --text:       [PRIMARY_TEXT];      /* e.g. #0f1f3d */
  --arc:        [ACCENT_HEX];        /* primary accent */
  --gold:       [SECONDARY_HEX];     /* secondary highlight */
  --arc-soft:   rgba(R,G,B,.09);
  --arc-border: rgba(R,G,B,.2);
  --code-bg:    rgba(R,G,B,.05);
  --code-text:  [DARK_ACCENT_HEX];
}
```

Hex-grid page background — swap `%23XXXXXX` with your URL-encoded accent hex:

```css
body::before {
  content: ''; position: fixed; inset: 0; z-index: 0; pointer-events: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='56' height='100'%3E%3Cpolygon points='28,2 54,17 54,47 28,62 2,47 2,17' fill='none' stroke='%23[ACCENT_HEX_NO_HASH]' stroke-width='0.4' opacity='0.05'/%3E%3Cpolygon points='28,52 54,67 54,97 28,112 2,97 2,67' fill='none' stroke='%23[ACCENT_HEX_NO_HASH]' stroke-width='0.4' opacity='0.05'/%3E%3C/svg%3E");
  background-size: 56px 100px;
}
```

Page banner with newspaper background + semi-transparent theme gradient:

```css
.page-banner {
  background: url('img/newspaper-{name}.svg') center top / cover no-repeat;
  padding: 36px 32px 32px;
  position: relative; overflow: hidden;
  margin-bottom: 28px;
}
.page-banner::before {
  content: ''; position: absolute; inset: 0;
  background: linear-gradient(135deg,
    rgba(R1,G1,B1,.82) 0%,
    rgba(R2,G2,B2,.76) 50%,
    rgba(R3,G3,B3,.84) 100%);
}
```

> Tip: keep the alpha values around `.75–.82`. Lower = more newspaper visible; higher = flatter colour.

---

## Step 4 — Create `{name}.html`

Copy `youtuber.html` as your starting template. Key substitutions:

| Location | Change |
|---|---|
| `<title>` | `J.A.R.V.I.S. — {Name}` |
| `:root` block | Your theme from Step 3 |
| `body::before` | Your hex-grid colour |
| `.page-banner` CSS | Newspaper SVG + gradient overlay from Step 3 |
| Banner `<img src>` | `img/{character}.jpg` (or `.webp`) from Step 1 |
| Banner eyebrow | `J.A.R.V.I.S. · {Name} Module` |
| Banner title | Hero name (e.g. `Thor`) |
| Banner sub | `{Real Name} · [tagline] · [tagline]` |
| `fetch('{name}-data.json')` | Your data file name |
| Stats cards | Rename `.metric` cards to your product's KPIs |
| `connect-block` code sample | Show your JSON schema |
| `coming-soon` icon | Pick a relevant Bootstrap icon |
| `.card:hover` border/shadow | Use your accent colour |

Nav bar — update the `active` class on the correct `.pnav-item` and add your page to every other page's nav.

---

## Step 5 — Add to the Hub (`index.html`)

### 5a — Nav link

Add inside `.pnav-links` in `index.html` (and in every other page's nav bar):

```html
<a href="{name}.html" class="pnav-item {name}">🦸 {Name}</a>
```

Add the following CSS to `style.css` (shared stylesheet):

```css
/* rest state */
.pnav-item.{name} { color: rgba(R,G,B,.75); border-color: rgba(R,G,B,.22) }
/* hover + active state */
.pnav-item.{name}.active,
.pnav-item.{name}:hover {
  color: [ACCENT_HEX];
  border-color: rgba(R,G,B,.5);
  background: rgba(R,G,B,.08);
  box-shadow: 0 4px 18px rgba(R,G,B,.25);
  transform: translateY(-2px);
}
/* active-page glow pulse */
@keyframes glow-{name} {
  0%,100% { box-shadow: 0 2px 8px rgba(R,G,B,.2) }
  50%      { box-shadow: 0 5px 22px rgba(R,G,B,.45) }
}
.pnav-item.{name}.active { animation: glow-{name} 2.8s ease-in-out infinite }
```

### 5b — Hub card

Add inside `.hub-grid` in `index.html`:

```html
<a href="{name}.html" class="hub-card card-{name}">
  <div class="card-poster">
    <img src="img/{character}.jpg" alt="{Hero Name}" loading="lazy">
    <div class="card-overlay">
      <div class="card-overlay-badge">🦸 {Name}</div>
      <div class="card-overlay-body">
        <div class="card-overlay-hero">{Hero Name}</div>
        <div class="card-overlay-name">{Real Name}</div>
        <div class="card-overlay-status" id="{name}-stats">Loading…</div>
      </div>
    </div>
    <div class="card-cta">Open {Name} →</div>
  </div>
</a>
```

Add card CSS inside the `<style>` block of `index.html`:

```css
.card-{name} { border: 3px solid rgba(R,G,B,.3) }
.card-{name}:hover {
  border-color: rgba(R,G,B,.75);
  box-shadow: 0 20px 70px rgba(R,G,B,.35);
}
.card-{name} .card-poster { background: linear-gradient(160deg, [LIGHT], [MID], [DARK]) }
.card-{name} .card-cta { border-color: rgba(R,G,B,.7); background: rgba(R,G,B,.3) }
```

### 5c — Status fetch

Add a new `try/catch` block inside `checkSystems()` in `index.html`:

```js
try {
  const r = await fetch('{name}-data.json?t=' + Date.now());
  if (r.ok) {
    const d = await r.json();
    active.{name} = d.connected === true;
    document.getElementById('{name}-stats').innerHTML = active.{name}
      ? '<span style="color:#059669">● Live</span>'
      : '<span style="color:#d97706">● Push {name}-data.json to activate</span>';
  } else throw new Error();
} catch(e) {
  document.getElementById('{name}-stats').innerHTML =
    '<span style="color:#d97706">● Not configured</span>';
}
```

Also add `{name}: false` to the `active` object at the top of `checkSystems()`, and update the `n === 3` count check to match the new total number of personas.

---

## Step 6 — Create `{name}-data.json`

Minimum schema (extend to match your product):

```json
{
  "generated_at": "2026-01-01T00:00:00Z",
  "connected": false,
  "stats": {},
  "feed": []
}
```

Set `"connected": true` to activate the live view and hide the "awaiting connection" placeholder.

---

## Step 7 — Push Data from Your Project

Your project needs write access to `jarvis-dashboard`. Add `DASHBOARD_PAT` (a GitHub PAT with `contents:write` on `jarvis-dashboard`) as a secret, then use this GitHub Actions step:

```yaml
- name: Push data to J.A.R.V.I.S. dashboard
  env:
    DASHBOARD_PAT: ${{ secrets.DASHBOARD_PAT }}
  run: |
    git clone https://x-access-token:${DASHBOARD_PAT}@github.com/jarvisthebot01123-bot/jarvis-dashboard.git /tmp/dash
    cp your-output.json /tmp/dash/{name}-data.json
    cd /tmp/dash
    git config user.name "github-actions[bot]"
    git config user.email "github-actions[bot]@users.noreply.github.com"
    git add {name}-data.json
    git diff --cached --quiet && exit 0
    git commit -m "data: update {name} $(date -u +%Y-%m-%dT%H:%M)Z"
    git push origin main
```

---

## File Checklist

- [ ] `docs/img/{character}.jpg` (or `.webp`) — portrait comic cover art ≥ 800 × 1200 px
- [ ] `docs/img/newspaper-{name}.svg` — themed newspaper hero background
- [ ] `docs/{name}.html` — product dashboard page
- [ ] `{name}-data.json` in `jarvis-dashboard` repo — live data feed
- [ ] `docs/index.html` — hub card + nav link + CSS + status fetch updated
- [ ] `docs/style.css` — nav item colours + glow animation added
- [ ] `DASHBOARD_PAT` secret added to your project's GitHub repo
