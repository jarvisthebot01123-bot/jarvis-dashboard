# Adding a New J.A.R.V.I.S. Persona

Each persona is a self-contained product page (`{name}.html`) that reads from its own JSON file (`{name}-data.json`). To add a new one, follow these 5 steps.

---

## Step 1 — Design Your Superhero Avatar (SVG)

Paste this prompt into Claude to generate a 48×48 SVG avatar:

```
Create a 48×48 inline SVG avatar for a Marvel-style superhero character.
Character concept: [DESCRIBE — e.g. "Thor, Norse god of thunder, golden hair, red cape, Mjolnir"]

Requirements:
- viewBox="0 0 48 48", width="48" height="48"
- Dark circular background: <circle cx="24" cy="24" r="23" fill="[DARK_BG_HEX]"/>
- Recognisable at small sizes: bold shapes, high contrast, minimal detail
- Primary theme colour: [HEX]  Secondary: [HEX]
- Semi-realistic comic style — clean SVG paths only, no external images
- Output ONLY the <svg>…</svg> element, no HTML wrapper
```

Replace `[DARK_BG_HEX]`, `[HEX]` with your theme colours before sending.

---

## Step 2 — Define Your CSS Theme

Add this block to your `{name}.html` (or a shared stylesheet):

```css
/* body class: theme-{name} */
:root {
  --bg:        [PAGE_BG];          /* e.g. #070d19 (dark) or #fdf5f3 (light) */
  --surface:   [CARD_BG];          /* e.g. rgba(7,10,20,.90) */
  --border:    [BORDER_COLOR];     /* e.g. rgba(0,100,255,.2) */
  --muted:     [SECONDARY_TEXT];   /* e.g. #7b8faa */
  --text:      [PRIMARY_TEXT];     /* e.g. #e8edf5 */
  --arc:       [ACCENT];           /* primary glow / link colour */
  --gold:      [SECONDARY_ACCENT]; /* secondary highlight */
  --accent-bg: rgba(R,G,B,.12);
}
```

Hex-grid pattern — swap `%23XXXXXX` with your accent colour (URL-encoded `#`):

```css
body::before {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='56' height='100'%3E%3Cpolygon points='28,2 54,17 54,47 28,62 2,47 2,17' fill='none' stroke='%23ACCENT_HEX' stroke-width='0.4' opacity='0.10'/%3E%3C/svg%3E");
  background-size: 56px 100px;
}
```

---

## Step 3 — Create `{name}.html`

Copy `youtuber.html` as your starting template. Key changes:

| Location | Change |
|---|---|
| `<title>` | `J.A.R.V.I.S. — {Name}` |
| `<body>` | keep as-is (no class needed — CSS variables in `:root`) |
| Hero avatar | paste your SVG from Step 1 |
| `.hero-sub` text | your persona subtitle |
| `.hero-desc` text | one-line description |
| `DATA_URL` (in `<script>`) | `'{name}-data.json'` |
| Stats cards | rename to your product's KPIs |
| `connect-block` code sample | show your JSON schema |

---

## Step 4 — Create `{name}-data.json`

Minimum schema (extend as needed):

```json
{
  "generated_at": "2026-01-01T00:00:00Z",
  "connected": false,
  "stats": {},
  "feed": []
}
```

---

## Step 5 — Add to the Hub (`index.html`)

**Persona nav button** — add inside `.persona-nav`:

```html
<a href="{name}.html" class="pnav-btn {name}">
  [avatar SVG 16×16]  🦸 {Name}
</a>
```

**CSS for the button** — add to `index.html` `<style>`:

```css
.pnav-btn.{name} { border-color: rgba(R,G,B,.4); color: #ACCENT_HEX; }
.pnav-btn.{name}:hover { background: rgba(R,G,B,.12); box-shadow: 0 4px 20px rgba(R,G,B,.2); }
```

**Card** — add inside `.grid`:

```html
<a href="{name}.html" class="card card-{name}">
  <div class="card-avatar"> [avatar SVG 44×44] </div>
  <h3>🦸 {Name}</h3>
  <p>One-line description of this AI product</p>
  <div class="card-stats" id="{name}-stats">Setup required</div>
  <br><span class="card-badge">{Hero Name}</span>
</a>
```

**Card CSS** — add to `index.html`:

```css
.card-{name} { --c: #ACCENT_HEX; border-color: rgba(R,G,B,.2); }
.card-{name}:hover { border-color: rgba(R,G,B,.55); box-shadow: 0 8px 40px rgba(R,G,B,.18); }
.card-{name} .card-avatar { background: rgba(R,G,B,.12); border: 1.5px solid rgba(R,G,B,.3); }
.card-{name} .card-badge  { background: rgba(R,G,B,.15); color: #ACCENT_HEX; }
```

---

## Step 6 — Push Data from Your Project

Your project needs write access to `jarvis-dashboard`. Add the `DASHBOARD_PAT` secret (GitHub PAT with `contents:write` on `jarvis-dashboard`), then use this GitHub Actions step:

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

Set `"connected": true` in your JSON to activate the live data view and hide the "awaiting connection" placeholder.

---

## File Checklist

- [ ] `{name}.html` — product dashboard page
- [ ] `{name}-data.json` — live data feed (pushed by your project)
- [ ] Hub `index.html` updated — nav button + grid card + CSS
- [ ] `DASHBOARD_PAT` secret added to your project's GitHub repo
