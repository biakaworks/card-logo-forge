# Card Logo Forge

A browser tool for the **Bless Thy Pulls** MTG series. Type a card name, pick a
metal style, customize the gradient, optionally stamp the TCGplayer price and a
commander synergy under it, and download a transparent PNG (video overlays) or
SVG (merch/print). Runs entirely in the browser — no build step.

## Styles
Thrash (chrome) · Brand White · Gothic (blackletter) · Death (blood) · Druid (green/bronze)

## Features
- Card-name autocomplete (full Scryfall catalog; built-in starter list as fallback)
- Per-style gradient editor + one-tap preset palettes
- Optional price line (TCGplayer market price via Scryfall, daily)
- Optional commander-synergy line (EDHREC) — needs the proxy below
- PNG (2048px transparent) and SVG (font-embedded vector) export

## Use it
Live: https://forge.biakaplays.com
Or open `index.html` locally in any browser.

## Optional: EDHREC synergy auto-fill (Cloudflare Worker)
EDHREC has no public API and blocks browser requests, so synergy auto-fill needs
a tiny free proxy. The synergy box still works without it — just type the
commander manually.

To enable auto-fill:
1. Sign in at https://dash.cloudflare.com → **Workers & Pages** → **Create** → **Create Worker**.
2. Name it (e.g. `edhrec-proxy`), click **Deploy**, then **Edit code**.
3. Replace the default code with the contents of `edhrec-proxy-worker.js`, then **Deploy**.
4. Copy the worker URL (looks like `https://edhrec-proxy.YOURNAME.workers.dev`).
5. In `index.html`, near the top of the `<script>`, set:
   `const EDHREC_PROXY="https://edhrec-proxy.YOURNAME.workers.dev";`
6. Re-upload `index.html`.

Test the worker directly in a browser:
`https://edhrec-proxy.YOURNAME.workers.dev/?card=Krenko, Mob Boss`
You should see `{"commander":"...","slug":"krenko-mob-boss"}`.

## Notes
- Prices baked into an export are a snapshot (TCGplayer data updates ~daily).
  Use priced PNGs the same day; don't rely on them for long-lived SVGs.
- Logos use real fonts, so spelling is always exactly what you type. For
  illustrated looks (vines, wings, skulls), use an AI image generator instead.
